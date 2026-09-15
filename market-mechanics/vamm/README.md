---
description: >-
  Rates Exchange virtual AMM lets users swap variable interest-rate exposure for
  fixed-rate exposure. This section is a technical overview of how Rates
  Exchange vAMM facilitates fixed for float swaps.
---

# Pricing & Mark Rates

A rates market has an annualized implied rate, a value for the remaining-term obligation, and prices used for execution and risk checks. These quantities serve different purposes.

## Rate and remaining-term value

An annualized rate expresses a cost over a year. The fixed payment represented by a contract depends on the time remaining until expiry. If the implied rate stays unchanged, the value of the remaining fixed obligation declines as the term runs out.

This does not mean the annualized rate itself must decline toward zero. At expiry, it is the remaining term that has ended.

## The virtual curve

The vAMM uses virtual reserves and a constant-product pricing relationship. Trading changes the reserve relationship and therefore the quoted value. Time decay accounts for the shrinking remaining term.

Virtual reserves describe the pricing curve. They should not be confused with an equal amount of spendable collateral or a promise of unlimited liquidity.

## Execution and risk prices

Execution occurs against the liquidity available to a trade. Risk checks use a mark intended to avoid relying solely on an instantaneous price.

A time-weighted average reflects prices over a window. It can differ from the current executable rate, particularly when market conditions change. Opening checks and liquidation checks should be interpreted according to their own rules.

## Near expiry

A small remaining cash value can correspond to a substantial change when expressed as an annualized rate. Review both remaining term and executable size rather than judging liquidity from an APR alone.

See [Swaps](swaps.md), [Market Specifications](../../rates-trading/market-specifications.md), and [Collateral Accounting](../position-health.md).

<a id="vamm"></a>
<a id="core-design"></a>
