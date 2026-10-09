# Fees

| Fee | Basis |
| --- | --- |
| Trading fee | A share of the collateral exchanged, always paid in collateral |
| Open interest (OI) fee | An annualized rate on open notional |
| Vault early-withdrawal fee | A share of net assets withdrawn before maturity |
| Gas fee | Per action, paid from a separate gas balance |

Fee rates are set per market and can change. The current values are shown in the app.

## Trading fee

The trading fee is always paid in the market's collateral token (USDC or USDT), never in notional. It is charged on the collateral leg of the trade, which is the fixed payment exchanged at entry or the closing payment on exit, so longs and shorts of the same size pay similar fees.

**Taker trades** (vAMM trades and market orders):

- **Buying (opening a long or closing a short):** the fee is added on top of the collateral you pay. You receive the full notional.
- **Selling (opening a short or closing a long):** the fee is deducted from the collateral you receive.

**Limit orders** (makers):

- **Bids:** placing the order locks the order size plus the maker fee. When it fills, you pay both and receive the full notional. The maker fee rate is fixed when the order is placed; later rate changes apply only to new orders.
- **Asks:** the fee is deducted from the collateral you receive when the order fills.

Taker and maker rates are set per market. The first markets launch with a taker fee of 5 bps and a maker fee of 0. The trading fee is separate from price impact, OI fees, and gas costs.

**Example:** a market order for **$1,000,000 in notional** with 30 days remaining at 5% APR. The fixed payment is $1,000,000 × 5% × 30 / 365 = $4,110, and the 5 bps taker fee on it is $2.05.

- A long pays $4,110 + $2.05 = **$4,112.05** and receives the full $1,000,000 in notional.
- A short receives $4,110 − $2.05 = **$4,107.95** into its position collateral.

## Open interest fee

The OI fee is an **annualized rate**, accruing every 12-second epoch while your position remains open. It is calculated on your **open notional**, not your collateral balance.

```text
OI fee = Open notional × Annual OI fee rate × Holding period in years
```

The holding period uses a 365-day year. The rate is set per market; the first markets launch at **15 bps annualized**.

**Example:** a position with **$100,000 in notional** held for 30 days at 15 bps:

```text
$100,000 × 0.0015 × 30 / 365 = $12.33
```

If you partially close the position, subsequent fees accrue on the remaining open notional.

## Vault early-withdrawal fee

Withdrawing before maturity incurs a fee of **1% of net**. The fee stays in the vault, benefiting the remaining depositors. It does not go towards protocol fees.

Vault withdrawals have a **15-minute delay** from the withdrawal request, both before and after maturity. Exposure limits can also restrict withdrawals.

<a id="gas-balances"></a>

## Gas fee

Swaps, deposits, and withdrawals typically cost about **$0.01 per action**, separate from trading and OI fees.

Gas is paid from a separate, pre-funded balance in the market’s collateral token: **USDC for USDC markets and USDT for USDT markets**.

When the gas balance falls below the minimum, supported flows can automatically top it up from your funding account and, if needed, your wallet.

<a id="fee"></a>
