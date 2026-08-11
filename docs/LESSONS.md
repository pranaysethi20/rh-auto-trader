# Lessons (the mistakes that made the rules)

This system's rules were not designed up front — they were *paid for*. Each one traces to a specific
logged mistake. Documenting them is the point: a system that visibly learns.

## Trading lessons

1. **Don't chase strength at the highs.** The two biggest single losses came from buying breakouts
   after they'd already run (a +25% 4-day pop; a breakout at the day's high that then gapped down
   through the stop). Rule: buy pullbacks to support, never the extension.

2. **Let winners run — cutting them early is worse than a loss.** Banked a +7% winner that had ~+20%
   left in it by trailing the stop too tight. The rare big winner is where the month's money is;
   don't cap it.

3. **Size stops to the stock's volatility (ATR-wide).** A stop trailed only ~3.7% below on a name
   that swings ~4%/day is a coin-flip tag — got whipsawed out, then it bounced. Give a stop ≥ ~1.5×
   the daily range, and don't tighten same-day after a green morning.

4. **Overnight gaps beat stops — half-size gappy names.** Two positions gapped *through* their stops
   overnight, filling well below the stop price. Stops cap damage but don't prevent gap slippage;
   size accordingly.

5. **Perfectionist entries miss trades.** Held a buy-limit at a "perfect" breakout number that the
   stock never quite touched — it found support a bit higher and ran without us. Enter at *real*
   support, not a prettier number that may never print.

6. **A monthly/deadline number causes bad trades.** Almost every loss traced to "we're behind, do
   something" energy. The target is a direction; it never justifies a trade you wouldn't otherwise
   take. Forcing it is how a flat month becomes a badly negative one.

## Systems / operations lessons

1. **Whole shares are mandatory for resting stops.** Fractional shares can't hold a stop order at
   all on Robinhood — so a high-priced stock in a small account leaves the position unprotectable.
   Pick low-priced volatile names.

2. **One owner per position.** Two agents both managing the same stock raced each other and placed
   conflicting orders. Exactly one agent owns any position's orders.

3. **Only automate exact, mechanical rules.** An agent once sold a winner early because it executed a
   vague, prose rule ("rotate if it lags"). Autonomous execution is allowed only on unambiguous
   conditions; judgment calls are escalated to a human.

4. **Verify orders after placing; kill stale ones.** A one-time task fired even after being disabled
   and left a stale order that silently reserved buying power and blocked the next trade. Always
   re-pull orders after acting, and cancel anything stale.

5. **Loud failure, never silent.** A broker auth token expired and the system went dark for five
   days with no signal. Now a dead connection is itself an alarm.

6. **Cash settlement (T+1) is a real constraint.** Proceeds from a sale aren't spendable until the
   next day; plan rotations around it, and don't assume freed cash is immediately deployable.

## The meta-lesson

The account survived a brutal stretch — a sector bear market, a choppy tape, multiple stop-outs, a
multi-day outage — down only single digits. That's *survival*, which is the precondition for the
good stretch. Discipline doesn't make losses impossible; it makes them small, survivable, and
boring, so the occasional real winner actually counts.
