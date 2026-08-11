# RH Auto-Trader

A phone-controlled, semi-autonomous single-stock trading system built on top of a Robinhood
"Agentic" brokerage account and a set of scheduled AI agents. It trades one volatile stock at a
time using fixed, pre-defined levels; protects every position with a resting broker stop; and is
fully controllable from an iPhone via a secure two-way notification channel.

> **Status:** live experiment on a small (~$500) account. This is a learning/research project, not
> investment advice. Expected value of short-term trading a small account is roughly flat — the
> value here is *discipline, tooling, and learning*, not guaranteed returns.

---

## What it does, in one picture

```
        ┌──────────────── THE MAC (must stay on) ────────────────┐
        │                                                          │
  rgti-autopilot ──► enters, protects, takes profit, re-arms       │
        │             one stock, mechanically, no human            │
        │                                                          │
  drift-detector ──► "levels stale, suggest E/S/T"  ───────────────┼──► 📲 phone
        │                                                          │
  volatility-scanner ──► "top 3 volatile names today" ────────────┼──► 📲 phone
        │                                                          │
  move-alert / pulse / close-summary ──► fills, stops, EOD ────────┼──► 📲 phone
        │                                                          │
  command-poller ◄─────────────────────────────────────────────────┼──◄ 📲 phone texts
        │            (status / cut / levels / buy / pause)          │
        └──────────────────────────────────────────────────────────┘
```

**Autonomous:** entries, stops, profit-taking, re-entry on wins, monitoring, alerts, weekly review.
**Human (a phone tap):** approve a level change, pick which stock to rotate to, cut a position.

---

## Repo contents

| File | What's in it |
|---|---|
| `README.md` | This overview |
| `docs/STRATEGY.md` | The trading strategy + risk doctrine |
| `docs/ARCHITECTURE.md` | Every scheduled agent and how they fit together |
| `docs/COMMANDS.md` | The two-way phone command channel + reference |
| `docs/LESSONS.md` | Hard-won lessons (the mistakes that made the rules) |

---

## Core design principles

1. **Trade one volatile stock at a time.** Master one name's rhythm instead of scattering.
2. **Fixed levels, no emotion.** Every trade has three numbers set *before* entry: entry (at
   support), stop (just below support), target (at resistance). No trade without all three.
3. **Whole shares only.** Fractional shares can't hold resting stops on Robinhood, so the stock's
   price must be low enough that ~$240 buys several whole shares.
4. **The broker stop is the only true 24/7 protection.** Everything else (the agents) runs only
   while the app is open; the resting GTC stop lives on Robinhood's servers.
5. **Never auto-rebuy a loser.** After a stop-out, the system stops and waits for a human. Winning
   re-entries are automatic; losing ones need eyes. This is the single non-negotiable safety rule.
6. **Humans keep the strategic levers.** Re-leveling and rotation are approved by a person — a bot
   that auto-updates its own levels and picks its own stocks with no oversight is how accounts die.

---

## Honest limitations

- **The Mac must stay on with the app open**, or the agents don't run. No true 24/7 without it.
- **The broker connection token expires periodically** and only a human can re-authorize it.
- **Small account, no proven edge.** Automation makes it *disciplined and tireless*, not *magic*.
  It cannot manufacture returns that aren't there.

---

## Secrets (NOT stored in this repo)

The command channel's secret topic name, passphrase, and the brokerage account number are
deliberately **kept out of this repo** (placeholders shown in the docs). They live only in the
local private notes / the agent memory file. Never commit them — anyone with the topic + passphrase
can send trade commands.
