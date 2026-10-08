# Vault Mechanics

The vault backs vAMM exposure. See [Architecture & Routing](../bootstrap-liquidity.md#order-routing) for its role in execution.

## Shares and value

Deposits receive shares representing a proportional interest in the vault’s NAV. Redemption converts those shares into assets at the applicable share value.

Net asset value, or NAV, is the vault's deposited capital plus the income it has actually banked:

```text
NAV = deposited capital, net of withdrawals + settlement PnL + fees
Share price = NAV / outstanding shares
```

NAV is floored at zero. Settlement PnL is the floating settlement the vault receives or pays on its net exposure. Fees include the vault's share of execution fees, liquidation penalties, and early-withdrawal fees, less any liquidation shortfalls.

**Implied-rate moves do not change NAV.** Opening, closing, and re-pricing positions leave NAV unchanged apart from fees: the cash exchanged when the vault takes a position is offset one for one by the value of that position, so the price of the vault's inventory never enters NAV.

## Income and losses

The vault's income includes its share of vAMM execution fees, the funding spread on matched exposure, and most of each [liquidation penalty](../liquidation.md#liquidation-bonus). An early-withdrawal fee, where applicable, is retained by the vault.

The vault also receives or pays floating settlement on its net exposure. Favorable settlement can add income; adverse settlement can reduce value. Liquidation shortfalls reduce share backing through [vault losses](vault-guardrails.md#vault-losses).

## Redemption and capacity

Redemption converts shares into their applicable NAV, after fees. Final settlement at maturity updates NAV to include remaining income and losses.

- [Provide Vault Liquidity](../../user-guides/provide-vault-liquidity.md): Withdrawal timing and participation steps.
- [Fees](../../rates-trading/fee.md#vault-early-withdrawal-fee): Early-withdrawal charges.
- [Vault Guardrails](vault-guardrails.md): Exposure limits on trades and withdrawals.

See [Settlement](../vamm/settlement-accrual.md) for floating-payment accounting.

<a id="slp-vault"></a>
<a id="core-functions"></a>
<a id="vault-lp-payout"></a>
