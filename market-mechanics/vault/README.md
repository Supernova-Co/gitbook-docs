# Vault Mechanics

The Rates Exchange vault supplies the capital behind vAMM execution. It takes the opposite side of the flow executed through that venue and participates in absorbing market losses.

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

The vault also receives or pays floating settlement on its net exposure. Favorable settlement can add income; adverse settlement can reduce value. When liquidation proceeds are insufficient to cover a position's closing cost, losses absorbed by the vault also reduce the backing of LP shares.

## Exposure constraints

Exposure limits constrain new trades and withdrawals based on the capital backing the vault’s obligations. See [Vault Guardrails](vault-guardrails.md).

## Deposits and withdrawals

Deposits receive shares based on the vault's valuation. A redemption exchanges shares for their applicable value, after any withdrawal charges.

A withdrawal request and its payout are separate stages. Redemption requires a **15-minute delay** after the withdrawal request, both before and after maturity. An exit before maturity incurs an early-withdrawal fee of **1% of net**, retained by the vault. Exposure restrictions can prevent a withdrawal when removing capital would leave the vault unable to support its obligations.

At maturity, final settlement updates the NAV used for redemption, including accumulated income and losses.

## Further reading

- [Provide Vault Liquidity](../../user-guides/provide-vault-liquidity.md)
- [Liquidation & Loss Allocation](../liquidation.md)
- [Settlement](../vamm/settlement-accrual.md)

<a id="slp-vault"></a>
<a id="core-functions"></a>
<a id="vault-lp-payout"></a>
