# Lend with Yield Boost

<a id="yield-boost"></a>
<a id="what-is-yield-boost"></a>

Yield Boost combines lending on Aave with a short rates position on Rates Exchange. It aims to improve your yield by supporting fixed-rate borrowing while your capital stays in Aave earning variable yield.

<a id="why-lenders-like-it"></a>

## Set your rate while you keep earning

Place a short-rate limit order at your target fixed rate through the **Yield Boost page on Rates Exchange**.

- **While you wait:** Your capital continues earning Aave’s variable lending yield.
- **If it fills:** The short locks in your selected fixed rate or better for the filled amount.
- **No fill, no trading fee:** If the order never fills, you keep earning Aave’s variable yield without entering the rates position. Gas costs still apply to applicable actions.

<a id="how-the-economics-work"></a>

The filled short receives its fixed payment for the term at entry, credited to the short's collateral, and pays the floating borrow rate over its term. Your Aave deposit earns the lending rate, so the selected fixed rate is not the exact combined yield. Sizing, rate differences, and fees affect your return.

## Example

You deposit **100,000 USDC** on Aave. Pool utilization is **80%** and the reserve factor is **10%**, so your deposit earns 72% of the borrow rate (80% × 90%). Yield Boost sizes the short to match that exposure:

```text
Short notional = 100,000 × 80% × (1 − 10%) = 72,000
```

Your limit order fills at a **6.5% fixed rate** with **30 days** until expiry. The fixed payment for the term is credited to the short's collateral at entry:

```text
Fixed payment = 72,000 × 6.5% × 30 / 365 = $384.66
```

Over the 30 days, the floating payments the short makes offset the Aave interest your deposit earns:

| | Borrow rate averages 4% | Borrow rate averages 8% |
| --- | --- | --- |
| Aave lending interest | +$236.71 | +$473.42 |
| Floating payments made by the short | −$236.71 | −$473.42 |
| Fixed payment received at entry | +$384.66 | +$384.66 |
| **Net over 30 days** | **+$384.66** | **+$384.66** |

In both cases you earn $384.66, a **4.68%** annualized yield on the full deposit (6.5% × 72%), before fees. At a 4% borrow rate, the same deposit without the boost would have earned $236.71 (2.88%).

The offset is exact only while utilization stays at 80%. If utilization changes, your Aave interest and the short's floating payments no longer match exactly.

## Get started

1. Open **Yield Boost**, connect your wallet, and choose a supported Aave lending market.
2. Review the short’s size, target fixed rate, expiry, required collateral, and fees.
3. Fund the required collateral on Rates Exchange, authorize trading, and place your limit order. Check its fill status before treating the hedge as active.

## Manage your position

- **Collateral:** The short needs separate collateral and can be liquidated. Monitor its health and add collateral or reduce exposure when needed; your Aave deposit does not automatically back it.

<a id="withdrawing-the-underlying-deposit"></a>

- **Withdrawals:** Your deposit remains subject to Aave’s risks and withdrawal rules. Withdrawing it does not cancel a waiting order or close a filled short. Review both when changing your deposit.

<a id="closing-the-hedge"></a>

- **Exit:** Cancel any unfilled order amount or close the filled short at available market terms. Closing can incur fees and leaves your Aave deposit unchanged.
- **Expiry:** Floating payments stop at the end of the term. The short's remaining balance is not returned automatically; [withdraw it](../../rates-trading/payments-and-pnl.md#at-expiry) yourself. **Auto-roll is upcoming and is not currently available.**

## Further reading

- [Fund & Withdraw](../../get-started/fund-and-withdraw.md)
- [Managing Collateral](../../rates-trading/interactive-blocks.md)
- [PnL](../../rates-trading/payments-and-pnl.md)
- [Fees](../../rates-trading/fee.md)
