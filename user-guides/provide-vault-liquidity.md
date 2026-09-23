# Provide Vault Liquidity

Rates Exchange vaults provide liquidity for rates trading through the vAMM. Deposit capital to receive vault shares and participate in the vault’s PnL.

- **How it works:** The vault takes the other side of vAMM trades and provides backing for liquidations.
- **PnL:** Trading fees, funding income, position gains or losses, and liquidation shortfalls contribute to the vault’s PnL.
- **Share value:** Your shares represent a portion of the vault’s capital and accumulated PnL. Profits increase their value; losses reduce it.
- **Withdrawal delay:** After requesting a withdrawal, wait for the required period before redeeming your shares.
- **Withdrawal limits:** Exposure limits can restrict withdrawals to keep enough capital backing open positions.
- **Early-withdrawal fee:** Withdrawing before maturity incurs a fee of **1% of net**. The fee stays in the vault, benefiting the remaining depositors.

## Further reading

- [Vault Mechanics](../market-mechanics/vault/README.md)
- [Vault Guardrails](../market-mechanics/vault/vault-guardrails.md)
- [Liquidation & Loss Allocation](../market-mechanics/liquidation.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
- [Lend with Yield Boost](../fixed-rate-borrowing/fixed-rate-yield-boost/README.md)
