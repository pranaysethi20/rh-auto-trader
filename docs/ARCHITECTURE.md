# Architecture

The system is a set of **scheduled AI agents** (cron-style tasks) that run on the local machine while
the Claude app is open. Each is a self-contained prompt that reads shared state from a memory file,
pulls live data from the Robinhood MCP connector, acts, and pushes notifications to the phone via
[ntfy](https://ntfy.sh).

## Shared state

- **Memory file** — a single markdown file is the source of truth: current strategy, levels, open
  positions, the risk doctrine, and the running log. Every agent reads it first; any agent that
  takes a material action updates it. This prevents stale-state bugs (an agent trading month-old
  positions) and keeps all agents consistent.
- **Broker (Robinhood MCP)** — the authoritative live state (positions, orders, quotes). When memory
  and the broker disagree, the broker wins.

## The agents

| Agent | Cadence | Role |
|---|---|---|
| **autopilot** | every 30 min, market hours | Full-loop execution of the active stock: arm entry → place stop on fill → sell at target → re-arm after a win. No auto-rebuy after a stop. |
| **command-poller** | every 10 min, 7am–11pm daily | Two-way phone control. Polls the secret command topic, validates the passphrase, executes commands (status / cut / levels / buy / pause / resume). See `COMMANDS.md`. |
| **drift-detector** | 2× daily, weekdays | Detects when the fixed levels have drifted out of line with how the stock is actually trading, and pushes *proposed* new levels to approve with one text. Detect + propose only. |
| **volatility-scanner** | daily, weekday morning | Ranks a universe of volatile, affordable, liquid names; pushes the top 3 rotation candidates with mapped entry/stop/target + ready buy commands. Proposes only. |
| **move-alert** | every 30 min, market hours | Watches held positions for big moves / stop proximity / unprotected positions / stop fills / a dead connection, and alerts. Places a protective stop if it ever finds one missing. Excludes the autopilot's stock (one owner only). |
| **account-pulse** | 3× daily | Verdict-first account snapshot + stop verification + goal pacing. |
| **close-summary** | weekday ~4:05pm | End-of-day summary to the phone: account value vs goal, each position's day result, what's next. |
| **weekly-doctrine-review** | Saturdays | Recursive self-review: grades each strategy rule by its real outcomes, demotes/rewrites the losers, logs a changelog, and does a pace check vs the monthly goal. Keeps the rules from going stale or rigid. |

## Key design decisions

- **One owner per position.** Exactly one agent manages any given stock's orders, to avoid two
  agents racing and double-placing/cancelling (a bug that happened early on).
- **Mechanical rules only for autonomous execution.** Agents may act autonomously only on exact,
  verifiable conditions (a price level, a fill event). Fuzzy/judgment rules ("rotate if it lags")
  are escalated to a human, never executed — an early agent once sold a winner off a vague rule.
- **Idempotency.** Order-placing agents check current state first and never place duplicates; a
  dedup guard prevents re-executing the same phone command twice.
- **Loud failure.** A dead broker connection is itself an alert — the system never fails silently.
- **The resting broker stop is the floor.** Everything else is "early awareness between stops."

## Notification channels (ntfy)

- **Outbound (alerts → phone):** a topic the phone subscribes to; all fills, proposals, and summaries
  land here.
- **Inbound (commands → system):** a *separate secret* topic the phone publishes to (via an iOS
  Shortcut) and the command-poller reads. Protected by an unguessable topic name **and** a
  passphrase prefix on every command.

## Hard constraints

- Agents run **only while the app is open**. Cloud execution isn't viable because the broker
  connector authenticates through the interactive desktop login.
- The broker **auth token expires** periodically and needs a human to re-authorize.
- The account is **cash-settled (T+1)** — proceeds from a sale aren't spendable until the next day,
  which shapes how fast the system can rotate.
