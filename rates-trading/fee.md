# Fees

Review the costs of entering, holding, and exiting a position together. The quoted implied rate is not a complete statement of the total cost or return.

## Trading costs

vAMM swaps carry an execution fee when opening or closing a position, including execution used to unwind a liquidation. The fee is distinct from price impact. An early entry and exit involve separate executions.

A share of vAMM swap fees supports the vault. Do not assume the entire fee is paid to LPs or that every execution venue has the same fee treatment.

## Settlement costs

The settlement fee is applied as a spread around the underlying floating rate: shorts pay the floating rate plus the funding fee, while longs receive the floating rate less the funding fee.

This spread is separate from the fixed payment exchanged at entry and from the fee for executing a trade. On matched exposure, both sides of the spread contribute to the vault’s fee income.

## Other actions

Liquidation charges are separate from ordinary execution charges. A vault redemption before maturity can also incur an early-withdrawal fee retained by the vault. Review the terms for the specific action rather than applying one trade example to every action.

Account-transfer costs are separate from these market and vault charges.

## Gas balances

Rates Exchange handles L2 gas through a pre-funded balance, so you do not pay network gas directly from your wallet for each action. Each collateral token has its own gas balance: USDC markets use USDC, and USDT markets use USDT.

Swaps, deposits, and withdrawals typically use about **$0.01 per action** from this balance. These gas costs are separate from trading and other fees.

If the balance falls below the minimum, these flows can automatically top it up using the same collateral token from your funding account and, if needed, your wallet.

## Comparing a quote with a result

Check the notional, remaining term, fixed payment, floating accrual, execution costs, and exit outcome. For a hedge, include the underlying lending or borrowing result as well.

A rate move measured in basis points cannot be compared directly with a cash fee without accounting for the size and duration of the exposure. See [Payments & PnL](payments-and-pnl.md).

<a id="fee"></a>
