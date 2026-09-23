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

The filled short receives fixed upfront and pays the floating borrow rate over its term. Your Aave deposit earns the lending rate, so the selected fixed rate is not the exact combined yield. Sizing, rate differences, and fees affect your return.

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
- **Expiry:** The short settles at the end of its term. **Auto-roll is upcoming and is not currently available.**

## Further reading

- [Fund & Withdraw](../../get-started/fund-and-withdraw.md)
- [Managing Collateral](../../rates-trading/interactive-blocks.md)
- [PnL](../../rates-trading/payments-and-pnl.md)
- [Fees](../../rates-trading/fee.md)
