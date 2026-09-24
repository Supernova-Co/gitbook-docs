# Vault Guardrails

Vault guardrails limit exposure relative to the capital backing the market.

## Exposure and capacity

New trades change the vault’s obligations; withdrawals reduce the capital backing them. Exposure checks can restrict either action when the resulting exposure exceeds the configured limit.

Blocking new exposure leaves existing positions in place. Liquidation and recovery mechanisms handle distressed positions and shortfalls separately.

## Withdrawal capacity

A withdrawal is blocked if the remaining backing would breach the exposure limit. This capacity check is separate from the [withdrawal delay and fee](../../user-guides/provide-vault-liquidity.md).

## Loss allocation and recovery

See [Vault Mechanics](README.md#shares-and-value) for the effect of losses on share value and [Liquidation & Loss Allocation](../liquidation.md#how-losses-are-allocated) for funding shortfalls, matched recovery, and ADL.

<a id="exposure-cap"></a>
<a id="phi-φ--partial-funding"></a>
<a id="price-per-share"></a>
<a id="maturity-settlement"></a>
