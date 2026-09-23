# Settlement

Settlement accounts for the fixed and floating obligations of rates positions across a market. It applies to market positions regardless of the venue that provided execution.

## Fixed and floating obligations

The long pays the fixed obligation upfront; the short receives it upfront. Floating payments then accrue according to the underlying rate over the holding period.

The floating side increases the long's balance and reduces the short's balance as it is accounted for.

## Accrual and balance updates

<a id="funding-accrual"></a>

An accumulated rate measure tracks growth in the underlying obligation over time. A position's notional and the growth since its previous accounting point determine the floating amount to account for.

Floating payments settle block by block into position balances. Wallet withdrawals are separate transactions.

## Closing and expiry

Closing and health checks account for outstanding floating accrual. At expiry, final settlement resolves the market's remaining obligations.

## Shortfalls

When vault backing cannot fund the net floating payment, settlement reduces long receipts through the funding factor `φ`. See [Liquidation & Loss Allocation](../liquidation.md).

For the trader's view, see [PnL](../../rates-trading/payments-and-pnl.md).

<a id="settlement-accrual"></a>
