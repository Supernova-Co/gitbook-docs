# Vault Guardrails

Vault guardrails limit exposure relative to the capital backing the market.

<a id="exposure-cap"></a>

## Exposure limits

The vault takes the other side of every vAMM trade, so its net position grows with user flow. Two limits keep that net exposure small relative to its capital:

| Vault position | Limit |
| --- | --- |
| **Net short** | The vault's net exposure, valued at the vAMM spot price, is capped at a configured share of its equity (capital plus PnL). |
| **Net long**  | The vault's net base outflow, recorded as negative PnL, is capped at a configured share of its capital. |

The limits scale with the vault's equity. As fees and funding grow it, the vault can take on more exposure. As maturity approaches, the same notional is worth less, so more of it fits under the same limit.

## What a breach blocks

- **Only trades that increase the vault's net exposure are blocked.** Trades that reduce it always pass, even when a limit is breached.
- **Trading continues on the order book.** When the vAMM leg is blocked, orders fill on the order book only. If the order book cannot fill the full size, the trade reverts.
- **Liquidations are never blocked**, whatever the vault's exposure.

Blocking new exposure leaves existing positions in place. Liquidation and recovery mechanisms handle distressed positions and shortfalls separately.

## Withdrawal capacity

Before maturity, an LP withdrawal is blocked if the vault would breach an exposure limit after it. This capacity check is separate from the [withdrawal delay and fee](../../user-guides/provide-vault-liquidity.md).

## Vault losses

If closing an underwater short cannot recover the amount owed, `accrueBadDebt` records the uncovered loss against the vault. LPs bear the reduction through the value backing their shares; see [Vault Mechanics](README.md#shares-and-value). Recorded vault assets are floored at zero. For the order in which losses are covered, see [Liquidation & Loss Allocation](../liquidation.md#how-losses-from-underwater-shorts-are-recovered).

<a id="matched-recovery"></a>
<a id="2-insufficient-funding-reduces-long-receipts"></a>

## Matched recovery

The market enters one-way matched recovery mode if the vault can no longer fund the net floating payments owed to longs, or if negative vault PnL exhausts its backing. Before maturity, entry into recovery trims the unmatched long exposure pro rata, leaving a 1:1 matched book in which shorts' floating payments fund longs directly. The vAMM is disabled and vault deposits are restricted.

**Risk valuation:** Liquidation eligibility in matched recovery uses a **3-day moving average of the underlying floating rate** instead of the normal vAMM TWAP, converted into a price for the remaining term:

```text
Matched-mode mark price = 3-day moving average of floating APR × Remaining duration in days / 365
```

The recovery latch is evaluated during transactions calling `Vault.settleFunding`.

<a id="phi-φ--partial-funding"></a>
<a id="price-per-share"></a>
<a id="maturity-settlement"></a>
