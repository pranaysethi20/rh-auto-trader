# Strategy & Risk Doctrine

## The trade

**Single-stock volatility range-trading with fixed limits.** Pick one cheap, volatile, liquid stock
and trade it repeatedly: buy near support, sell near resistance, cut fast if support breaks. The
edge isn't prediction — it's asymmetry (small fixed losses, larger winners) executed without emotion.

### The 5-step loop (works on any stock)

1. **Find the structure.** Pull the chart (2 weeks–3 months). Is it *ranging* or *trending*? Draw
   the line where it keeps bouncing up (**support**) and where it keeps getting rejected
   (**resistance**). Those two lines are 90% of the job.
2. **Name three numbers before buying.** Entry (at support), Stop (just below support — where you're
   proven wrong), Target (near resistance). Can't name all three? It's not a trade, it's a hope.
3. **Check the math.** Reward must be ≥ 2× risk. Below 2:1, skip it.
4. **Buy support, never the top.** If it's already run, you're late — wait for the pullback. Missing
   a trade is free; chasing one is expensive.
5. **Execute mechanically, then review.** Limit-buy in → stop-order the instant you fill → sell at
   target. Then log: *did I follow my own plan?* (the only thing you actually control).

### Mindset

- You're not predicting — you're reacting to levels. Buy fear (support), sell greed (resistance) —
  the opposite of instinct.
- The stop is the entry fee, not failure. Small losses, let winners run.
- No setup = no trade. Cash is a position.
- Grade decisions by process, not any single outcome. A good decision can have a bad outcome.

---

## Risk charter (hard rules)

- **Every position gets a protective resting stop at entry**, sized so any single loss is small
  (~5–8%).
- **One stock at a time**, whole shares, no margin, no leverage, no options.
- **Fixed levels only** — entry / stop / target defined before entry, executed mechanically.
- **Never auto-rebuy after a stop-out.** Support broke = setup invalid. Stop and wait for a human.
- **Capital-preservation floor:** if the account halves from its stake, switch to preservation mode
  (mostly cash, tiny high-conviction only), rebuild slowly.
- **Never force a trade to hit a number or a deadline.** Forcing trades is the fastest way to lose.

---

## What each rule cost to learn

Every rule above traces to a real, logged mistake — see `LESSONS.md`. The short version:

- *No chasing* ← bought breakouts at the highs, got stopped out repeatedly.
- *Let winners run* ← banked a +7% winner that had +20% in it (the worst kind of mistake).
- *ATR-wide stops* ← trailed a stop too tight on a volatile name and got whipsawed out.
- *Half-size gappy names* ← stops gapped through overnight, adding slippage.
- *Whole shares* ← a fractional position couldn't hold a resting stop at all.
- *Buy real support, not a perfect number* ← held out for a level that never printed and missed the
  whole move.

---

## The honest framing

Roughly flat expected value; no demonstrated prediction edge (daily market-call track record ran
well below a coin flip over a small sample). The strategy's job is to keep losses small and
survivable so that the occasional real winner actually moves the account — and to build the
discipline and tooling to run it tirelessly. The number goals (e.g. "+$X/month") are directions,
never promises, and never justify a bad trade.
