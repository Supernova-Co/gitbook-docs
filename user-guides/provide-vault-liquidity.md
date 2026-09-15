# Provide Vault Liquidity

The Rates Exchange vault supplies capital behind the vAMM. Vault participants share its economic results through their vault shares, including income and losses.

Vault participation is different from lending on Aave and adding a rates hedge. See [Lend with Yield Boost](../fixed-rate-borrowing/fixed-rate-yield-boost/README.md) for that strategy.

## How it works

Deposits receive shares representing a proportional interest in the vault. The vault takes the opposite side of trades executed through the vAMM and can bear losses from the market's liquidation and settlement mechanisms.

Share value depends on the vault's assets and accounting for its obligations and results. A displayed return is not a guaranteed payout.

## PnL and share value

The vault earns fee income and receives or pays settlement on its net exposure. It can also absorb losses when the backing of a liquidated position is insufficient. These results affect the assets backing vault shares.

Your economic interest is your share of the vault's value. It is not a fixed-rate lending deposit or a promise to return the original amount. See [Vault Mechanics](../market-mechanics/vault/README.md) for the NAV and share-price explanation.

## Deposits and withdrawals

A deposit receives shares. A withdrawal redeems shares at the applicable valuation, subject to the vault's rules and costs.

A redemption request is separate from payout. Withdrawals have a delay, an early exit can carry a fee, and exposure constraints can prevent capital from leaving the vault. Review the applicable conditions before requesting redemption.

Do not treat vault shares as an unused trading-account balance. Closing a rates trade and redeeming vault shares are different actions.

## Risks and limitations

The vault can lose money through its market exposure and its role in absorbing shortfalls. Guardrails constrain some actions; they do not guarantee principal or uninterrupted withdrawals.

## Further reading

- [Vault Mechanics](../market-mechanics/vault/README.md)
- [Vault Guardrails](../market-mechanics/vault/vault-guardrails.md)
- [Liquidation & Loss Allocation](../market-mechanics/liquidation.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
