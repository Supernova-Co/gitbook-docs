# Collateral Accounting

A rates account tracks available funds, position balances, and order reservations.

## Account concepts

| Concept | Meaning |
| --- | --- |
| Available balance | Funds not currently committed to a position or order |
| Position balance | Funds accounted for within a market position |
| Signed notional | The size and direction of rate exposure |
| Order reservation | Funds or exposure committed to a resting order |

In existing notation, `base` records a position balance and `quote` records signed notional. Positive notional denotes long exposure; negative notional denotes short exposure. Order reservations reduce available collateral or exposure.

Position balances change through trade cash flows, floating settlement, and collateral transfers. See [PnL](../rates-trading/payments-and-pnl.md) for cash flows and [Settlement](vamm/settlement-accrual.md) for accrual accounting.

## Initial and maintenance collateral

For a short, debt is the cost of closing its remaining exposure, and LTV compares that debt with eligible collateral:

$$
\text{Debt} = |N| \times P \qquad \text{LTV} = \frac{\text{Debt}}{C}
$$

where $$N$$ is the notional, $$P$$ the price per unit of notional for the remaining term, and $$C$$ the eligible collateral. Prices come from APRs:

$$
P = \text{APR} \times \frac{\text{days remaining}}{365}
$$

### Initial margin: open or modify a short

The opening check values debt at the **highest** of three prices:

$$
P_{\text{IM}} = \max\left(P_{\text{mark}},\ P_{\text{spot}},\ P_{\text{floor}}\right)
$$

$$
\text{LTV}_{\text{IM}} = \frac{|N| \times P_{\text{IM}}}{C_{\text{free}}} \le 33\%
$$

- $$P_{\text{mark}}$$: the [mark price](vamm/README.md#collateral-and-liquidation): the 15-minute TWAP of spot, or the 3-day moving average of the underlying floating rate in [matched recovery](vault/vault-guardrails.md#matched-recovery).
- $$P_{\text{spot}}$$: the current vAMM spot price.
- $$P_{\text{floor}}$$: the minimum collateral price; see [Floor margin](#floor-margin).
- $$C_{\text{free}}$$: position balance less funds reserved for orders.

### Maintenance margin: liquidation

$$
\text{LTV}_{\text{MM}} = \frac{|N| \times P_{\text{mark}}}{C} > 66\% \implies \text{liquidatable}
$$

- $$P_{\text{mark}}$$: the same mark price as in the initial margin.
- $$C$$: position balance after orders are cancelled and accrued payments are accounted for.

The gap between 33% and 66% is the buffer between opening a position and becoming liquidatable.

**Example:** 30 days remaining, $$N = \$1{,}000{,}000$$, mark APR 4.5%, spot APR 5%, floor below both.

$$
P_{\text{IM}} = \max(4.5\%,\ 5\%,\ \text{floor}) \times \tfrac{30}{365} = 0.411\% \;\Rightarrow\; \text{Debt}_{\text{IM}} = \$4{,}110
$$

$$
C_{\text{free}} \ge \frac{\$4{,}110}{33\%} = \$12{,}453 \text{ to open}
$$

At the 4.5% mark, liquidation debt is $$\$3{,}699$$, so the short becomes liquidatable if collateral falls below $$\$3{,}699 / 66\% = \$5{,}604$$.

### Why spot is included in initial margin, not maintenance margin

Margin usually uses a smoothed price, since spot can jump on a single trade. Only shorts can be liquidated, and their risk rises only when the price goes up, so taking the higher of mark and spot at opening is safely conservative. Maintenance excludes spot so that brief price pushes cannot trigger liquidations.

### Floor margin

A minimum margin requirement ensures that positions opened in the final **5 days before maturity cannot be liquidated**. The floor applies to opening and modification checks; it does not raise the liquidation threshold.

## Withdrawals

See [Managing Collateral](../rates-trading/interactive-blocks.md#adding-or-withdrawing-collateral) for withdrawal health checks and [Orders & Execution](order-book.md#withdrawals) for open-order restrictions.

<a id="position-health"></a>
<a id="health-ratio"></a>
<a id="two-ltv-thresholds"></a>
<a id="funding-erodes-collateral-first"></a>
