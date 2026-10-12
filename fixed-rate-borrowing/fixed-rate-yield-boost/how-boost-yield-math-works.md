# How Boost Yield Math Works

## The two legs

| Leg | Venue | You receive | You pay |
|---|---|---|---|
| Lending | Aave | Floating supply yield | — |
| Short rate | Rates Exchange | Fixed rate | Floating rate |

A **short** on Rates Exchange means you **receive fixed** and **pay floating** for the chosen term.

The floating you earn from Aave and the floating you pay on Rates Exchange are built to **offset each other**, leaving the fixed rate as your yield on the boosted slice. The sections below show the cashflows, and what changes when pool utilization drifts after the short opens.

---

## The cashflows

### Aave lending

On Aave, for a deposit of size $L$, you receive per unit time:

$$
L \cdot r_{\text{supply}} = L \cdot (1 - rf) \cdot u_{\text{now}} \cdot r_{\text{borrow, now}}
$$

where $rf$ is the Aave **reserve factor**, $u_{\text{now}}$ is pool **utilization**, and $r_{\text{borrow, now}}$ is the floating **borrow rate**. Utilization and borrow rate are **live**: they move with the pool after you boost.

### Rates Exchange short

To boost a deposit of size $L$, Yield Boost opens a **short with notional**:

$$
N = L \cdot (1 - rf) \cdot u_{\text{open}}
$$

$u_{\text{open}}$ is the pool **utilization at open**. It sizes the short so that, at that moment, the short's floating payments equal the deposit's floating income.

For a market order, $u_{\text{open}}$ is Aave's live utilization. For a limit order, the fill time is not known in advance, so $u_{\text{open}}$ is the utilization Aave's rate curve implies at your limit rate. If utilization at fill differs from that estimate, the short is slightly larger or smaller than the floating income it covers, and the drift described below applies from the first day.

The short receives its fixed payment for the term at entry as a single amount, $N \cdot r_{\text{fixed}} \cdot \text{term}$, and pays floating on $N$ as it accrues. Expressed per unit time:

$$
\begin{aligned}
\text{pay (floating)} &= N \cdot r_{\text{borrow, now}} \\
\text{receive (fixed)} &= N \cdot r_{\text{fixed}}
\end{aligned}
$$

### Total on the boosted deposit

Adding the Aave leg and the two short legs:

$$
\text{Total} = L \cdot (1 - rf) \cdot u_{\text{now}} \cdot r_{\text{borrow, now}} + N \cdot \left( r_{\text{fixed}} - r_{\text{borrow, now}} \right)
$$

The first term is what the deposit earns on Aave anyway. The second term is what the boost adds or costs: the short's notional times the gap between the fixed rate you locked and the floating rate that actually prevailed.

Substituting $N$ gives the same total in terms of utilization:

$$
\text{Total} = L \cdot (1 - rf) \Big[ u_{\text{open}} \cdot r_{\text{fixed}} + r_{\text{borrow, now}} \cdot \big(u_{\text{now}} - u_{\text{open}}\big) \Big]
$$

If utilization never moves ($u_{\text{now}} = u_{\text{open}}$), the second bracket vanishes, the floating legs cancel exactly, and you earn the locked fixed rate on the boosted slice.

---

## What happens when utilization moves

Two different questions have two different answers. Keep them apart.

**Compared with the rate you locked.** Utilization decides this. If utilization rises above $u_{\text{open}}$, more of your deposit is earning floating than the short covers, so you earn **more** than the locked rate. If utilization falls, the short is now larger than your floating income, so you earn **less** than the locked rate.

**Compared with not boosting at all.** Utilization does not decide this. From the first total above, the boost adds exactly $N \cdot (r_{\text{fixed}} - r_{\text{borrow, now}})$. That is positive when the fixed rate you locked is above the borrow rate that prevailed, and negative when the borrow rate ends up higher than your fixed rate. Utilization only changes the size of the Aave income it is added to.

### Example

You deposit **100,000 USDC** with a **10%** reserve factor at **80%** utilization and lock **6.5%** fixed for **30 days**. The short's notional is 72,000 and its fixed payment, received at entry, is $384.66. The locked rate on the whole deposit is 6.5% × 90% × 80% = **4.68%**.

| | Utilization 80%, borrow rate 4% | Utilization 60%, borrow rate 4% | Utilization 95%, borrow rate 12% |
| --- | --- | --- | --- |
| Aave interest earned | +$236.71 | +$177.53 | +$843.29 |
| Floating paid by the short | −$236.71 | −$236.71 | −$710.14 |
| Fixed received at entry | +$384.66 | +$384.66 | +$384.66 |
| **Boosted total** | **$384.66 (4.68%)** | **$325.48 (3.96%)** | **$517.81 (6.30%)** |
| Same deposit without the boost | $236.71 (2.88%) | $177.53 (2.16%) | $843.29 (10.26%) |
| **What the boost added** | **+$147.95** | **+$147.95** | **−$325.48** |

In the second column utilization fell, so you earned less than the 4.68% you locked. You still came out ahead of not boosting, because 6.5% fixed beat the 4% borrow rate. In the third column utilization rose, so you earned more than the locked rate. You still came out behind not boosting, because the borrow rate climbed to 12% and you had sold 72,000 of that at 6.5%.

Within a single Aave rate curve, utilization and the borrow rate move together, so the common cases are the first two. The third shows what a rate spike does.

---

## Effective Supply APY

**Effective Supply APY** is the headline yield on your **entire** Aave balance for that asset, boosted and unboosted slices combined.

Each boost locks a **boost rate** on the slice you boosted:

$$
r_{\text{boost}} = (1 - rf) \cdot u_{\text{open}} \cdot r_{\text{fixed}}
$$

Effective Supply APY is the **size-weighted blend** of each boosted slice earning its locked $r_{\text{boost}}$ until its market matures and any remaining unboosted deposit earning the live supply rate $r_{\text{supply}}$, compounded over the time to maturity and expressed as one annual rate on the whole balance. It assumes utilization stays at each slice's $u_{\text{open}}$; the section above describes what changes when it does not.
