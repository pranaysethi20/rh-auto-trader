# Journey & Performance Log

A running, honest record of the experiment: what we traded, what happened, what we learned, and
how the system evolved. Updated as we go. The point is to *see the pattern over time* — not any
single trade.

---

## Where it started

- **Seed:** ~$200, later topped up to ~$500 total deposited.
- **Original goal:** grow it aggressively. Evolved into a monthly $ target, then — honestly —
  retired in favor of an **execution-scored** goal: judge whether we followed the plan, and let
  P&L be the byproduct.
- **Core realization:** roughly flat expected value, no prediction edge. The value is discipline,
  tooling, and learning. That reframing is the most important thing that happened.

## The system that emerged

A phone-controlled, semi-autonomous single-stock volatility trader. See `ARCHITECTURE.md`. Built
across ~2 months, mostly the hard way — every rule traces to a logged mistake (`LESSONS.md`).

## Trade log

| Date | Ticker | In | Out | Result | Note |
|---|---|---|---|---|---|
| Jun | HOOD | — | — | +$18.58 | first winner |
| Jun | IBKR | $96 | $94.15 | −$3.70 | small loss, rotated |
| Jun–Jul | AFRM | $77.81 | $82.88 | +$15.75 | trailed too tight, left ~$20 on the table |
| Jul | RKLB | $100.12 | $90.61 | −$28.55 | chased a V-bounce; gapped through stop |
| Jul | OSCR | $31.74 | $29.19 | −$5.10 | chop stop-out |
| Jul | HOOD | $113.50 | $101.05 | −$24.90 | breakout, gapped down overnight |
| Jul | OXY | $54.44 | ~$54 | ~flat | war-premium energy; task sold early (bug, fixed) |
| Aug | KRE | $76.56 | $76.65 | +$0.28 | exited on a bounce vs an open-dump — patience paid |
| Aug | RGTI | — | — | never filled | wouldn't pull back; rotated to RIOT |
| Aug | RIOT | (armed $19.30) | — | open | current focus — a real range-trade |

> Keep appending. One line per trade: date, ticker, entry, exit, result, one-line lesson.

## Milestones

- **Discipline doctrine** written and made recursive (weekly self-review grades the rules).
- **Full-loop autopilot** — enters, protects, takes profit, re-arms — built and verified.
- **Two-way phone control** via ntfy + iOS Shortcut — verified working autonomously.
- **Drift-detector + volatility-scanner** — the system proposes re-levels and rotation candidates.
- **First live rotation** (RGTI → RIOT) driven by "this stock trends, that one ranges."

## What we're tracking going forward

- **Per-trade:** did we follow the plan? (entry at support / stop set / let winner run) — Y/N.
- **Vehicle fit:** is the current ticker *ranging* (good) or *trending* (rotate)?
- **Account curve:** value over time vs deposited base — is discipline producing flat-to-green?
- **Rule health:** which doctrine rules are earning their keep; prune the rest (weekly review).

## Honest scoreboard (update periodically)

- **Deposited:** ~$500
- **Account (last check):** ~$479
- **Net realized to date:** ≈ flat-to-slightly-negative
- **Read:** survived a brutal tape (chip bear market, chop, an outage) roughly intact. Survival is
  the precondition for the good stretch. The tooling and discipline are the real gains so far.
