# Open Interest Caps

Each market limits how much open interest each side can hold. The cap keeps a market at a size its liquidity can absorb while that liquidity is still growing.

## Why markets are capped

- **Liquidations stay absorbable.** Open interest that is large relative to the liquidity behind it cannot be closed at a reasonable price. The cap keeps the largest possible liquidation within what the vault and order book can absorb.
- **The oracle stays honest.** The oracle rate comes from the underlying market, so open interest here must stay small relative to it. Otherwise a position could be large enough to pay for moving the underlying market itself.
- **Unknown risks stay bounded.** Any exploit or manipulation not caught by other safeguards still needs open interest to be profitable, so the cap limits its maximum payoff.

## How the cap changes over time

The cap applies separately to the long side and the short side. It grows as maturity approaches, in line with the vAMM's depth: as contracts get cheaper, the market can absorb more of them in a forced close.

```text
Cap = Starting cap × min(Maximum multiple, √(Market term / Time remaining))
```

The cap stops growing once it reaches its maximum multiple of the starting cap and stays flat until maturity. The starting cap and maximum multiple vary from market to market, and Rates Exchange can also set the cap manually.

## When a side reaches its cap

- **Trades that increase a side's open interest above its cap revert.** This includes order-book matches that open new positions on both sides.
- **Trades that keep open interest equal or lower always pass**, even when the market is above its cap. Closing a position is never blocked by the cap.
- **Liquidations, foreclosures, and auto-deleveraging are never blocked** by the cap.
- **In [matched recovery](vault/vault-guardrails.md#matched-recovery), open interest can only shrink.**

## Related mechanics

- [Liquidation & Loss Allocation](liquidation.md)
- [Vault Guardrails](vault/vault-guardrails.md)
- [Market Parameters](key-parameters.md)
