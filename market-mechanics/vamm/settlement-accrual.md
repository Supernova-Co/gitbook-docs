# Settlement

Settlement updates position balances across a market, regardless of whether trades filled on the order book or vAMM. For payment direction and cash-flow accounting, see [PnL](../../rates-trading/payments-and-pnl.md#settlement-pnl).

## Accrual accounting

<a id="funding-accrual"></a>

Floating payments accrue every **12-second epoch**. Each market keeps an accumulated rate measure that tracks growth in the underlying obligation over time. A position's floating payment is its notional multiplied by the growth in that measure since the position was last settled:

```text
Floating payment = |notional| × (accumulated rate now − accumulated rate at last settlement)
```

<a id="lazy-settlement"></a>

## Lazy settlement

Payments accrue every epoch for every position, but they are written into a position's balance only when that position is next settled, instead of for every position every 12 seconds. A single settlement applies everything accrued since the previous one.

- **Actions on the position settle it first.** Trades, order fills, and liquidations apply outstanding accrual before they change the position or check its health.
- **Anyone can settle any position.** A public settlement call applies a position's outstanding accrual without changing anything else.
- **Stored balances can lag.** Until a position is settled, its stored balance does not yet reflect recent payments. For a short, the true balance is lower than the stored one.

The health shown in the app and the health that liquidation bots monitor both include payments that are not yet settled, so a short can be liquidated even if its stored balance still looks healthy.

If a short's accrued payments exceed its remaining collateral when it is settled, the excess is recorded as a loss against the vault. See [Liquidation & Loss Allocation](../liquidation.md#how-losses-from-underwater-shorts-are-recovered).

## Related mechanics

- [Implied Rate & Mark Rate](README.md#which-rate-is-used): Rate inputs for execution, risk checks, and floating payments.
- [Collateral Accounting](../position-health.md): How accrual affects balances and health.
- [PnL: Closing and expiry](../../rates-trading/payments-and-pnl.md#close-position): Closing cash flows and final settlement.
- [Fees: Open interest fee](../../rates-trading/fee.md#open-interest-fee): Fees accrued while a position remains open.

<a id="settlement-accrual"></a>
