# Liquidation & Loss Allocation

Liquidation addresses a short position that no longer meets the market's health requirements. Loss allocation describes what happens when available backing cannot meet all obligations. These are related but different questions.

## Why a short can become liquidatable

The cost of closing the remaining short can rise, while floating payments can reduce its collateral over time. A short therefore needs monitoring even when the implied rate has not moved sharply.

## Closing or transferring exposure

Liquidation can involve closing exposure through market execution or transferring exposure to another adequately backed participant. The applicable process determines what happens to the position, collateral, and any charges.

Outstanding orders and floating accrual matter when evaluating the position. A displayed balance before accounting for them is not a complete measure of its condition.

## Vault losses

When the vault absorbs a shortfall, its value can fall. LPs bear that effect through their interest in the vault. A mechanism that prevents negative recorded vault value does not make the economic loss disappear.

## Participant payment risk

If the market cannot meet its floating obligations in full, longs may receive less than expected. A long's prepaid fixed obligation removes an unpaid fixed liability; it does not guarantee the floating receipts needed for a hedge.

Keep payment-shortfall risk distinct from liquidation of the long itself and from liquidation of an underlying loan.

## What to monitor

Short holders should monitor health and accrual. Hedgers should consider what reduced or interrupted receipts would mean for their underlying exposure. Vault participants should consider both counterparty exposure and market shortfalls.

See [Collateral, Health & Liquidation](../rates-trading/interactive-blocks.md), [Vault Guardrails](vault/vault-guardrails.md), and [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md).

<a id="liquidation"></a>
<a id="standard-flow"></a>
<a id="liquidation-flow"></a>
<a id="foreclosure-flow"></a>
