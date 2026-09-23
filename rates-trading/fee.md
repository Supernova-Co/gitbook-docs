# Fees

| Fee | Rate |
| --- | --- |
| Trading fee | 1 bp |
| Open interest (OI) fee | 15 bps annualized |
| Vault early-withdrawal fee | 1% of net |
| Gas fee | Typically $0.01 per action |

## Trading fee

The trading fee is **1 bp**. It is separate from price impact, OI fees, and gas costs.

## Open interest fee

The OI fee is **15 bps annualized**, accruing block by block while your position remains open. It is calculated on your **open notional**, not your collateral balance.

```text
OI fee = Open notional × 0.0015 × Holding period in years
```

**Example:** For a position with **$100,000 in notional** held for 30 days, using a 365-day year:

```text
$100,000 × 0.0015 × 30 / 365 = $12.33
```

If you partially close the position, subsequent fees accrue on the remaining open notional.

## Vault early-withdrawal fee

Withdrawing before maturity incurs a fee of **1% of net**. The fee stays in the vault, benefiting the remaining depositors. It does not go to the protocol’s fee wallet.

Withdrawals also remain subject to the vault’s withdrawal delay and exposure limits.

<a id="gas-balances"></a>

## Gas fee

Swaps, deposits, and withdrawals typically cost about **$0.01 per action**, separate from trading and OI fees.

Gas is paid from a separate, pre-funded balance in the market’s collateral token: **USDC for USDC markets and USDT for USDT markets**.

When the gas balance falls below the minimum, supported flows can automatically top it up from your funding account and, if needed, your wallet.

<a id="fee"></a>
