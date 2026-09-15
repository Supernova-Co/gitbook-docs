# Vault Mechanics

The Rates Exchange vault supplies the capital behind vAMM execution. It takes the opposite side of the flow executed through that venue and participates in absorbing market losses.

## Shares and value

Deposits receive vault shares; redemption exchanges shares for the value available under the vault's rules. Shares represent a proportional interest, not a promise to return the original deposit amount.

Net asset value, or NAV, brings together the vault's deposited capital and its realized and unrealized results:

```text
NAV = deposited capital, net of withdrawals + realized PnL + unrealized PnL
Share price = NAV / outstanding shares
```

These expressions describe economic quantities without implementation scaling. NAV is floored at zero. Realized PnL includes settled income and losses; unrealized PnL accounts for the value of remaining exposure.

A participant's share of NAV is not a separate guaranteed payout. Keep deposited principal, share value, and realized income distinct when reviewing a result.

## Income and losses

The vault's income includes its share of vAMM execution fees and the funding spread on matched exposure. An early-withdrawal fee, where applicable, is retained by the vault.

The vault also receives or pays floating settlement on its net exposure. Favorable settlement can add income; adverse settlement can reduce value. When liquidation proceeds are insufficient to cover a position's closing cost, losses absorbed by the vault also reduce the backing of LP shares.

A favorable fee stream does not guarantee a positive total return. The applicable revenue allocation and costs must be considered alongside the risks the vault carries.

## Exposure constraints

The vault's ability to support more flow is constrained. Some actions can be limited when exposure or losses are too large relative to its backing.

Guardrails constrain activity; they do not establish a guaranteed floor for LP returns. See [Vault Guardrails](vault-guardrails.md).

## Deposits and withdrawals

Deposits receive shares based on the vault's valuation. A redemption exchanges shares for their applicable value, after any withdrawal charges.

A withdrawal request and its payout are separate stages. Redemption is subject to a withdrawal delay, and an exit before maturity can carry an early-withdrawal fee. Exposure restrictions can prevent a withdrawal when removing capital would leave the vault unable to support its obligations.

Review the applicable timing and costs before requesting redemption. Withdrawable value can differ from deposited principal.

At maturity, settlement of remaining market obligations affects the value available to participants. Do not assume maturity restores prior losses.

## Further reading

- [Provide Vault Liquidity](../../user-guides/provide-vault-liquidity.md)
- [Liquidation & Loss Allocation](../liquidation.md)
- [Settlement](../vamm/settlement-accrual.md)

<a id="slp-vault"></a>
<a id="core-functions"></a>
<a id="vault-lp-payout"></a>
