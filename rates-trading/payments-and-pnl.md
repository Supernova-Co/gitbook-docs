# Payments & PnL

A rates position has both a payment history and a value at which it can be closed. Keep those separate when evaluating its result.

## Three parts of the result

| Component | What it represents |
| --- | --- |
| Fixed payment | The fixed obligation paid by the long and received by the short at entry |
| Floating payments | The underlying-rate accrual received by the long and owed by the short during the holding period |
| Closing value and costs | The value realized when reducing or closing the remaining exposure, together with applicable charges |

For a hedge, also include the interest paid on the underlying loan or earned on the lending deposit. The Rates Exchange position alone does not show the result of the combined strategy.

## Implied-rate changes

An open long generally benefits in exit value from a rise in the implied rate; an open short generally benefits from a fall. This describes the value of the remaining exposure, not a guaranteed total profit.

The time left until expiry matters. Comparing two quoted rates without accounting for remaining term does not establish a cash profit or loss.

## Floating accrual

Floating payments accumulate over the period the position is open. They increase a long's balance and reduce a short's balance as they are accounted for.

Accrued amounts and completed transfers are different concepts. Funds becoming part of a position's accounting does not necessarily make them immediately withdrawable.

## Closing and expiry

An early close is executed against the remaining rate exposure. Prior floating accrual remains part of the position's economic history and must not be counted twice.

At expiry, there is no remaining term to trade. Final settlement determines the position's remaining balance and obligations.

## Reading the result

Review entry payments, accrued floating payments, closing proceeds or costs, and fees together. Distinguish the result of the rates position from the result of an underlying loan, lending deposit, or vault investment.

See [Settlement](../market-mechanics/vamm/settlement-accrual.md), [Closing & Expiry](integrations.md), and [Fees](fee.md).
