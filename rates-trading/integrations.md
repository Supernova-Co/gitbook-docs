---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Closing & Expiry

An early close exits the remaining rate exposure at available execution terms. Expiry ends the market's term. Neither action automatically repays an underlying loan or withdraws an underlying lending deposit.

## Closing early

A close offsets the existing exposure with the opposite direction for the same market and remaining term. The execution rate can differ from the original rate.

Check the size being closed and review any remaining position or resting orders afterward. Do not assume a request to close guarantees execution at a particular rate.

## Payments and closing value

Floating accrual during the holding period is part of the position's payment history. Closing also realizes the value of its remaining exposure. Count each component once when reviewing the result, together with fees.

See [Payments & PnL](payments-and-pnl.md).

## At expiry

At the market's expiration, no remaining term is left to trade. Final settlement accounts for the position's remaining obligations and balance. Review the completed settlement before treating funds as available to withdraw.

## Continuing a hedge

A hedge has a defined expiry. Continued exposure requires a position covering the next period. **Auto-roll is upcoming and is not currently available.** A new position may have a different rate or execution terms.

If the underlying Aave loan or deposit remains open, it continues under that protocol's terms.

## Withdrawing afterward

Closing or settling a rates position and transferring available funds out of the account are separate steps. See [Fund & Withdraw](../get-started/fund-and-withdraw.md).

<a id="close-position"></a>
