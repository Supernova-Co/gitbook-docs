---
description: How implied rates, mark rates, and floating rates determine execution, risk valuation, and payments.
---

# Implied Rate & Mark Rate

- **Implied rate** is the annualized fixed rate quoted by the market. The Terminal displays the AMM spot implied rate, reflecting the latest AMM trade.
- **Mark rate** is a 15-minute time-weighted average used for collateral and liquidation checks.
- **Floating rate** is the underlying market’s rate, supplied by the oracle and used to calculate floating payments.

## Which rate is used?

| Calculation | Rate used |
| --- | --- |
| Terminal implied rate | AMM spot implied rate |
| Trade execution | The rates at which the order fills on the order book or vAMM |
| Open or modify a short | Highest of mark rate, spot rate, and the [minimum collateral rate](../position-health.md#floor-margin) |
| Short liquidation eligibility in normal trading | Mark rate |
| Short liquidation eligibility in [matched recovery](../vault/vault-guardrails.md#matched-recovery) | 3-day moving average of the underlying floating rate |
| Floating settlement PnL | Floating rate |
| Realized position PnL | Actual entry and exit execution rates, position sizes, and remaining terms |

The **liquidation trigger** uses the applicable risk mark. In normal trading, the subsequent liquidation closes exposure at available market prices, which can differ from the mark.

## Implied rate

The vAMM calculates its marginal implied rate from its virtual reserves and the remaining time to maturity:

```text
Spot price = Virtual base reserve / Virtual quote reserve
Time to maturity in years = Remaining duration in days / 365
Implied APR = Spot price / Time to maturity in years
```

**Spot price** is the fixed payment per [Debt Unit](../bootstrap-liquidity.md#debt-unit) for the remaining term: the interest one DU earns in the lending market between now and maturity, compounding included. **Implied APR** expresses that payment as a simple yearly rate on the DU's value at market open, using a **365-day year**. Partial days count proportionally.

Two consequences of that definition:

- The floating interest a position receives compounds, while the quoted rate does not compound out to a full year. Against the APR a lending app shows, the difference on a one-month market at current rates is under 0.01 percentage points.
- Because the rate is measured on the DU's value at market open and that value grows as interest accrues, later in a market the quoted rate reads slightly above the real cost. On a one-month market at current rates the gap is under 0.02 percentage points.

**Example:** With 90 days remaining and a spot price of 0.0125:

```text
Implied APR = 0.0125 / (90 / 365) ≈ 5.07%
```

At that price, $100,000 in notional corresponds to a $1,250 fixed payment before fees and price impact.

A vAMM trade changes the reserve ratio, so its average execution rate depends on trade size and curve depth. Order-book fills execute at matched order rates. An order can fill across both venues.

## Mark rate

The mark rate is a **15-minute time-weighted average of implied APR observations from AMM trades**. Each observation is weighted by how long it prevailed within the window.

```text
Mark APR = Sum(Implied APR × Duration) / Total duration
```

**Example:** If implied APR is 4% for 10 minutes and 5.5% for the next 5 minutes:

```text
Mark APR = (4% × 10 + 5.5% × 5) / 15 = 4.5%
```

For risk calculations, the mark APR is converted into a remaining-term price the same way as the spot price above: the mark price is the mark APR multiplied by the time to maturity in years.

Time weighting smooths short-lived changes in the live implied rate. Trades still execute at current venue prices.

**Initialization:** The TWAP starts at the vault’s initialization rate, set slightly above fair value.

## Price deviation cap

The spot-to-mark deviation cap is a per-market parameter expressed in percentage points of implied APR.

After each routed trade, the protocol checks the difference between spot implied APR and mark APR:

- **Increasing deviation:** The trade reverts if it increases deviation beyond the cap.
- **Reducing deviation:** The trade passes this check even if the remaining deviation is still above the cap. Other execution and collateral checks still apply.

**Example:** With a mark APR of 5%, the band is 3%–7%. A trade moving spot APR from 6% to 7.1% reverts. A trade reducing spot APR from 7.5% to 7.2% passes the deviation check.

## Collateral and liquidation

Each rate above is converted into a price for the remaining term before it is used in a health check. See [Collateral Accounting](../position-health.md#initial-and-maintenance-collateral) for the margin requirements and health calculations.

## Further reading

- [Collateral Accounting](../position-health.md)
- [Liquidation & Loss Allocation](../liquidation.md)
- [vAMM pricing](../bootstrap-liquidity.md#vamm-pricing)
- [Settlement](settlement-accrual.md)
- [PnL](../../rates-trading/payments-and-pnl.md)

<a id="vamm"></a>
<a id="core-design"></a>
