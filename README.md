# Solana Homebase — Agentic Treasury

> **Superteam Earn — Agentic Engineering Grant (Tranche 2 deliverable)**
> An autonomous treasury manager for AI agents that settles on **Solana**.

**Status, 2026-11-23 — verified by running it, not by remembering it:**

```
python3 tranche2_demo.py --fast      # exits 0 only if every quote came back
  SOL: $5 USDC -> 0.069387 SOL       (Jupiter, live)
  TAO: $5 USDC -> 0.02601  TAO       (Jupiter, live)
```

The quote path needs **no signing library and no wallet** — stdlib only. Execution needs a funded
keypair (`SOLANA_REAL=1`). If any quote fails, the demo now says `INCOMPLETE` and **exits 2**; the
previous version printed tracebacks and then announced *"Live quotes verified above."*


## The Loop
```
Agent earns USDC via x402 (any chain)
      ↓
Bridge USDC → Solana (Across, sub-5s, ~0.08%)
      ↓
Treasury deploys USDC on Solana (regime-gated: yield vs trade)
      ↓
Agent pays services from Solana wallet (sub-cent gas, 200ms)
      ↓
Q402 trust receipt on every payment
```

## Why Solana is the homebase
- **USDC settlement is the point** — sub-second, sub-cent, native.
- **Cheaper than bridging** — agents pay on the destination chain directly.
- Matches the grant's own requirement: "live MVP + some Solana integration."

### ⭐ The real advantage: the Solana DeFi community
Solana isn't just a fast ledger — it's a **liquidity network with its own builder
communities**. An agentic treasury on Solana taps into:
- **Meteora** — dynamic liquidity pools + concentrated LP strategies
- **Orca** — the concentrated-liquidity DEX, tight-range yield
- **Raydium** — the central AMM + staking/farms
- **+ 30 more routed through Jupiter** (Phoenix, Jito, etc.)

One Solana wallet reaches the whole ecosystem through Jupiter — no bridging
between DEXs. That's the edge over EVM.

## What's here
| File | Purpose |
|------|---------|
| `solana_homebase.py` | Orchestrator: status / bridge / buy / pay. DRY_RUN by default, refuses to fake a trade. |
| `gta_solana_leg.py` | Jupiter swap leg (SOL/TAO). Live quotes verified. |
| `tranche2_demo.py` | One-command live proof for the grant reviewer. |
| `SPEC.md` | Full spec + funding requirements. |

## Live proof (Aug 5, 2026)
- `$5 USDC → 0.067 SOL` (Jupiter, live quote)
- `$5 USDC → 0.0252 TAO` (Jupiter, live quote)
- Across Base→Solana bridge: sub-5s, ~0.08% fee

## Run
```bash
python3 tranche2_demo.py            # full dry-run demo (safe)
python3 solana_homebase.py --action buy --symbol SOL --amount 5 --dry-run  # live quote
# To execute (Jordan greenlight only):
#   export SOLANA_PRIVATE_KEY=... SOLANA_REAL=1
#   python3 solana_homebase.py --action buy --symbol SOL --amount 5
```

## Funding to go live
- ~$2 SOL (gas) + ~$20 USDC on Solana (bridged from grant).

## Repos
- Solana contracts: `ProtoJay4789/agent-economy-solana`
- x402 gateway: `ProtoJay4789/x402-gateway`
- **This orchestrator: `ProtoJay4789/solana-homebase`**
