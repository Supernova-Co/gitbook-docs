# Vault Mechanics

The vault backs vAMM exposure. See [Architecture & Routing](../bootstrap-liquidity.md#order-routing) for its role in execution.

## Shares and value

Deposits receive shares representing a proportional interest in the vault’s NAV. Redemption converts those shares into assets at the applicable share value.

Net asset value, or NAV, brings together the vault's deposited capital and its realized and unrealized PnL:

```text
NAV = deposited capital, net of withdrawals + realized PnL + unrealized PnL
Share price = NAV / outstanding shares
```

These expressions describe economic quantities without implementation scaling. NAV is floored at zero. Realized PnL includes settled income and losses; unrealized PnL accounts for the value of remaining exposure.

## Income and losses

The vault's income includes its share of vAMM execution fees and the funding spread on matched exposure. An early-withdrawal fee, where applicable, is retained by the vault.

The vault also receives or pays floating settlement on its net exposure. Favorable settlement can add income; adverse settlement can reduce value. Liquidation shortfalls reduce share backing through [loss allocation](../liquidation.md#1-closing-shortfalls-reduce-vault-backing).

## Redemption and capacity

Redemption converts shares into their applicable NAV, after fees. Final settlement at maturity updates NAV to include remaining income and losses.

- [Provide Vault Liquidity](../../user-guides/provide-vault-liquidity.md): Withdrawal timing and participation steps.
- [Fees](../../rates-trading/fee.md#vault-early-withdrawal-fee): Early-withdrawal charges.
- [Vault Guardrails](vault-guardrails.md): Exposure limits on trades and withdrawals.

See [Settlement](../vamm/settlement-accrual.md) for floating-payment accounting.

<a id="slp-vault"></a>
<a id="core-functions"></a>
<a id="vault-lp-payout"></a>
