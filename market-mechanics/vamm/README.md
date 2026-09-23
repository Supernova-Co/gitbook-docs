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

At expiry, the remaining-term value reaches zero even if the quoted annualized rate is unchanged.

## The virtual curve

The vAMM uses virtual reserves and a constant-product pricing relationship. Trading changes the reserve relationship and therefore the quoted value. Time decay accounts for the shrinking remaining term.

Virtual reserves set curve depth; vault capital provides the backing for vAMM exposure.

## Execution and risk prices

Execution occurs against the liquidity available to a trade. Risk checks use a mark intended to avoid relying solely on an instantaneous price.

A time-weighted average reflects prices over a window. It can differ from the current executable rate, particularly when market conditions change. Opening checks use the highest of the time-weighted mark, spot price, and applicable price floor. Normal-mode liquidation checks use the time-weighted mark.

## Near expiry

Near expiry, a small change in remaining-term value can produce a large change in quoted APR because the annualization period is short.

See [Swaps](swaps.md), [Supported Markets](../../get-started/supported-markets.md), and [Collateral Accounting](../position-health.md).

<a id="vamm"></a>
<a id="core-design"></a>
