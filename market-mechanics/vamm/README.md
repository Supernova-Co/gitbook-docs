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
| Short liquidation eligibility in matched recovery | Floating rate, currently used as the forward mark |
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
| Open or modify a short | Highest of mark price, spot price, and the configured minimum collateral price |
| Liquidation eligibility in normal trading | Mark price |
| Liquidation eligibility in matched recovery | Forward mark, currently based on the floating rate |

```text
Short debt value = Absolute short notional × Risk price
LTV = Short debt value / Eligible collateral
```

Opening or modifying a short uses a stricter LTV threshold than the maintenance threshold used for liquidation.

**Floor margin:** A minimum margin requirement ensures that positions opened in the final **5 days before maturity cannot be liquidated**. The floor applies to opening and modification checks; it does not raise the liquidation threshold.

### Matched recovery

When insufficient vault backing triggers matched recovery, the vAMM is disabled. Before maturity, unmatched long exposure is reduced to leave matching long and short notional.

Liquidation eligibility then uses the **forward mark** instead of the normal vAMM TWAP. The current forward-rate input is the oracle-supplied floating rate, converted into a price for the remaining term:

```text
Forward mark price = Floating APR × Remaining duration in days / 365
```

See [Liquidation & Loss Allocation](../liquidation.md) for recovery mechanics.

## Time to maturity

At an unchanged implied APR, the fixed payment for the remaining term decreases as expiry approaches:

```text
Price = Implied APR × Remaining duration in days / 365
```

Between trades, `decayFixed` adjusts the virtual reserves while preserving the constant product and implied APR. At expiry, the remaining-term value reaches zero.

## Floating rate and PnL

Floating payments use the **oracle-supplied floating rate**. They settle block by block and continue even when the implied fixed rate is unchanged.

- **Settlement PnL:** Floating payments received by longs or paid by shorts.
- **Realized position PnL:** Entry and exit cash flows from the exposure traded.
- **Unrealized position PnL:** The estimated gain or loss on remaining open exposure.

See [PnL](../../rates-trading/payments-and-pnl.md) for the cash-flow calculations.

## Further reading

- [Collateral Accounting](../position-health.md)
- [Liquidation & Loss Allocation](../liquidation.md)
- [Settlement](settlement-accrual.md)

<a id="vamm"></a>
<a id="core-design"></a>
