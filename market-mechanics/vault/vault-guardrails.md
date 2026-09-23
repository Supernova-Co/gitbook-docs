# Vault Guardrails

Vault guardrails limit exposure relative to the capital backing the market.

## Exposure and capacity

New trades change the vault’s obligations; withdrawals reduce the capital backing them. Exposure checks can restrict either action when the resulting exposure exceeds the configured limit.

Blocking new exposure leaves existing positions in place. Liquidation and recovery mechanisms handle distressed positions and shortfalls separately.

## Trading and withdrawals

Execution depends on available venue capacity. A withdrawal can be blocked when removing capital would leave insufficient backing for open positions.

Vault redemptions also require a **15-minute delay**, both before and after maturity. See [Vault Mechanics](README.md) for redemption terms.

## Shortfalls and recovery

- **Vault losses:** Losses absorbed by the vault reduce NAV and share value.
- **Funding shortfalls:** The funding factor `φ` scales the vault-funded portion of long payments when backing is insufficient.
- **Matched recovery:** Entry into recovery disables the vAMM and restricts vault deposits. Before maturity, unmatched long exposure is trimmed pro rata to leave a matched book.

See [Liquidation & Loss Allocation](../liquidation.md) for the triggers and allocation rules.

<a id="exposure-cap"></a>
<a id="phi-φ--partial-funding"></a>
<a id="price-per-share"></a>
<a id="maturity-settlement"></a>
