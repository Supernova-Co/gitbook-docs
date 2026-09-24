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
| Short liquidation eligibility in normal trading | Mark rate |
| Short liquidation eligibility in [matched recovery](../liquidation.md#matched-recovery) | Floating rate, currently used as the forward mark |
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

**Spot price** is the fixed payment per unit of notional for the remaining term. **Implied APR** annualizes that payment using a **365-day year**. Partial days count proportionally.

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

The mark rate is converted into a remaining-term price for risk calculations:

```text
Mark price = Mark APR × Remaining duration in days / 365
```

Time weighting smooths short-lived changes in the live implied rate. Trades still execute at current venue prices.

**Initialization:** The TWAP starts at the vault’s initialization rate, set slightly above fair value.

## Price deviation cap

The current spot-to-mark deviation cap is **200 bps**, equivalent to **2 percentage points of APR**.

After each routed trade, the protocol checks the difference between spot implied APR and mark APR:

- **Increasing deviation:** The trade reverts if it increases deviation beyond the cap.
- **Reducing deviation:** The trade passes this check even if the remaining deviation is still above the cap. Other execution and collateral checks still apply.

**Example:** With a mark APR of 5%, the band is 3%–7%. A trade moving spot APR from 6% to 7.1% reverts. A trade reducing spot APR from 7.5% to 7.2% passes the deviation check.

## Collateral and liquidation

| Check | Price used |
| --- | --- |
| Open or modify a short | Highest of mark price, spot price, and the [minimum collateral price](../position-health.md#floor-margin) |
| Liquidation eligibility in normal trading | Mark price |
| Liquidation eligibility in [matched recovery](../liquidation.md#matched-recovery) | Forward mark, currently based on the floating rate |

See [Collateral Accounting](../position-health.md#floor-margin) for margin requirements and health calculations.

## Further reading

- [Collateral Accounting](../position-health.md)
- [Liquidation & Loss Allocation](../liquidation.md)
- [Swaps: Time decay](swaps.md#time-decay)
- [Settlement](settlement-accrual.md)
- [PnL](../../rates-trading/payments-and-pnl.md)

<a id="vamm"></a>
<a id="core-design"></a>
