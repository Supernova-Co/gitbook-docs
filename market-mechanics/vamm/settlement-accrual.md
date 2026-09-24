# Settlement

Settlement updates position balances across a market, regardless of whether trades filled on the order book or vAMM. For payment direction and cash-flow accounting, see [PnL](../../rates-trading/payments-and-pnl.md#settlement-pnl).

## Accrual accounting

<a id="funding-accrual"></a>

An accumulated rate measure tracks growth in the underlying obligation over time. The position’s notional and the change in that measure since its previous accounting point determine the floating payment to apply.

Closing and health checks account for outstanding floating accrual before evaluating the position. See [Collateral Accounting](../position-health.md) for how accrual affects balances and health.

## Funding shortfalls

When vault backing cannot cover the net floating payment, the funding factor `φ` scales the vault-funded portion of long payments. See [Liquidation & Loss Allocation](../liquidation.md#2-insufficient-funding-reduces-long-receipts) for the calculation and recovery triggers.

## Related mechanics

- [Implied Rate & Mark Rate](README.md#which-rate-is-used): Rate inputs for execution, risk checks, and floating payments.
- [PnL: Closing and expiry](../../rates-trading/payments-and-pnl.md#close-position): Closing cash flows and final settlement.
- [Fees: Open interest fee](../../rates-trading/fee.md#open-interest-fee): Fees accrued while a position remains open.

<a id="settlement-accrual"></a>
