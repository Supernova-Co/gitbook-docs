# PnL

Your rates position has two sources of PnL: **settlement PnL** from floating-rate payments and **position PnL** from changes in the value of your remaining exposure.

## Settlement PnL

Floating payments settle block by block, updating your position balance:

- **Long:** Receives floating payments.
- **Short:** Pays floating payments.

The amount depends on the underlying borrow rate, your position size, and the time held. Payments continue even when the market’s quoted fixed rate stays unchanged. They update your position balance rather than transferring to your wallet.

## Position PnL

The market’s implied fixed rate affects the value of your remaining position:

- **Long:** A rise in the implied fixed rate increases your position’s value; a fall decreases it.
- **Short:** A fall in the implied fixed rate increases your position’s value; a rise decreases it.

These describe rate changes with remaining time held constant. As expiry approaches, the remaining term also affects position value.

**At entry, a long pays fixed and a short receives fixed upfront.** This payment establishes the position’s entry value. Receiving fixed upfront is not immediate profit: the short still owes floating payments and has an open position to settle or close.

## Realized and unrealized PnL

Settlement and position PnL describe **where PnL comes from**. Realized and unrealized PnL distinguish gains and losses already accounted for from the changing value of open exposure.

- **Realized PnL:** Gains or losses already accounted for through floating-rate settlement or by closing exposure.
- **Unrealized PnL:** The estimated gain or loss on exposure you still hold, based on its current valuation.

Closing exposure realizes its position PnL. A partial close realizes only the portion closed. Realized position PnL depends on the execution price, which may differ from the mark used to display unrealized PnL.

Realized PnL does not necessarily mean withdrawable funds. Collateral requirements and open orders can still restrict withdrawals.

<a id="close-position"></a>

## Closing and expiry

**Closing early:** Trade in the opposite direction to reduce or close your position. Floating payments settled while you held it remain part of your PnL, alongside entry and exit cash flows.

<a id="at-expiry"></a>

**At expiry:** Floating accrual ends at maturity. Final settlement accounts for outstanding obligations and determines the remaining balance.

**Continuing exposure:** Open a position covering the next term. **Auto-roll is upcoming and is not currently available.**

## Total PnL

For a fully closed position, before fees:

| Direction | PnL calculation |
| --- | --- |
| **Long** | Floating payments received + payment received when closing − fixed payment paid at entry |
| **Short** | Fixed payment received at entry − floating payments paid − payment paid when closing |

Deduct applicable fees that are not already included in those amounts.

At expiry, the remaining exposure has no closing value. PnL comes from the difference between the upfront fixed payment and floating payments over the term, less fees.

## Further reading

- [Managing Collateral](interactive-blocks.md)
- [Fees](fee.md)
- [Fund & Withdraw](../get-started/fund-and-withdraw.md)
