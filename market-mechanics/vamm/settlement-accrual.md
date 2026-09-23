# Settlement

Settlement accounts for the fixed and floating obligations of rates positions across a market. It applies to market positions regardless of the venue that provided execution.

## Fixed and floating obligations

The long pays the fixed obligation upfront; the short receives it upfront. Floating payments then accrue according to the underlying rate over the holding period.

The floating side increases the long's balance and reduces the short's balance as it is accounted for.

## Accrual and balance updates

<a id="funding-accrual"></a>

An accumulated rate measure tracks growth in the underlying obligation over time. A position's notional and the growth since its previous accounting point determine the floating amount to account for.

Economic accrual, updating a stored position balance, and withdrawing funds are separate events. Describing accrual as continuous should not imply a continuous stream of wallet transfers.

## Closing and expiry

Before evaluating the outcome of a close or a health check, outstanding accrual must be considered. At expiry, final settlement resolves the market's remaining obligations.

For hedgers, this settlement does not settle the separate Aave loan or deposit.

## Shortfalls

Settlement depends on the ability of the market to meet its obligations. A shortfall can affect collateral, vault value, and amounts received by participants. See [Liquidation & Loss Allocation](../liquidation.md).

For the trader's view, see [Understanding PnL](../../rates-trading/payments-and-pnl.md).

<a id="settlement-accrual"></a>
