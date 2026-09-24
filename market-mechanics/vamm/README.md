---
description: How implied APR and the time-weighted mark are calculated and used for execution and collateral checks.
---

# Implied Rate & Mark Rate

**Implied rate** is the annualized fixed rate quoted by the market. **Mark rate** is a time-weighted average used to value positions for collateral and liquidation checks. Floating payments use the underlying borrow rate.

## Implied rate

The vAMM uses virtual base and quote reserves on a constant-product curve:

```text
k = baseReserve × quoteReserve
Spot price = baseReserve / quoteReserve
Implied APR = Spot price / Time to maturity in years
```

Spot price is the fixed payment per unit of notional for the remaining term. Implied APR annualizes that payment. These formulas omit token and fixed-point scaling.

**Example:** With 0.25 years remaining and a spot price of 0.0125 per unit of notional:

```text
Implied APR = 0.0125 / 0.25 = 5%
```

At that price, $100,000 in notional represents a $1,250 fixed payment before fees and price impact.

**Used for execution:** The reserve ratio gives the vAMM’s marginal quote. A swap moves the reserves, so its average execution rate depends on trade size and curve depth. Order-book fills execute at matched order rates; the router can combine both venues.

## Mark rate

The mark rate is a **15-minute time-weighted average** of implied APR observations from AMM trades. Each observation is weighted by how long that rate prevailed within the configured window:

```text
Mark APR = Sum(Implied APR × Duration) / Total duration
Mark price = Mark APR × Time to maturity in years
```

**Example:** If implied APR is 4% for 10 minutes and 7% for 5 minutes within the 15-minute window:

```text
Mark APR = (4% × 10 + 7% × 5) / 15 = 5%
```

The window is configured per market through `minPriceWindow`; the current setting is **15 minutes**.

**Used for risk valuation:** The mark price values the short’s remaining obligation. Time weighting smooths brief changes in the live quote; execution still uses current venue prices.

## Price deviation cap

The current cap is **200 bps**, measured as an absolute difference of **2 percentage points** between spot implied APR and mark APR.

After each routed trade, the protocol checks the spot-to-mark deviation. A trade reverts if it increases the deviation beyond the cap. Trades that reduce the deviation pass this check, including when the remaining deviation is still above the cap; other execution and collateral checks still apply.

**Example:** With a mark APR of 5%, the 200 bps band runs from 3% to 7%. A trade that moves spot APR from 6% to 7.1% reverts. A trade that reduces spot APR from 7.5% to 7.2% passes the deviation check.

The cap is configured per market through `maxTwapDivergenceAprWad`.

## Collateral and liquidation checks

| Check | Price used |
| --- | --- |
| Open or modify a short | Highest of mark price, spot price, and the applicable price floor |
| Liquidation eligibility in normal mode | Mark price |
| Liquidation eligibility in matched recovery mode | Forward mark |

```text
Short debt value = Absolute short notional × Risk price
LTV = Short debt value / Eligible collateral
```

Opening checks apply the stricter safe LTV threshold. Liquidation eligibility uses the maintenance LTV threshold. See [Collateral Accounting](../position-health.md) for collateral definitions and [Liquidation & Loss Allocation](../liquidation.md) for recovery rules.

## Time to maturity

Between trades, `decayFixed` adjusts the virtual reserves while preserving the constant product and implied APR. As the remaining term shortens, the fixed-payment price decreases:

```text
Price = Implied APR × Time to maturity in years
```

At expiry, the remaining-term value reaches zero. APR conversion applies only while time to maturity is positive.

## Floating settlement

The underlying market’s borrow rate determines floating payments. Implied APR sets the fixed side of a trade, while the mark rate provides the risk valuation. See [Settlement](settlement-accrual.md) for floating-payment accounting.

<a id="vamm"></a>
<a id="core-design"></a>
