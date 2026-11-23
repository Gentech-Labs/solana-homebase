# Solana as Homebase — Agentic Treasury MVP (Superteam Tranche-2 Deliverable)

**Status:** ✅ **BUILDING, VERIFIED 2026-11-23** — the quote rail runs end to end; on-chain execution
still gated on a funded Solana wallet. Two defects were found and fixed on 2026-11-23 by running the
demo it ships: (1) `gta_solana_leg.py` imported `requests`, which was never declared, so every quote
raised `ModuleNotFoundError` — while `tranche2_demo.py` printed *"Live quotes verified above"*;
(2) the demo's closing line was hardcoded, so it reported success over any failure.
**Both were the same class: a program asserting a result nobody measured.**
**Grant:** Superteam Earn Agentic Engineering — Tranche 2 unlock (second $100)
**Goal:** A live, working MVP with **Solana integration** + documentable $200 coding subs.

## Why Solana is the homebase
- **USDC settlement is the point** — Solana does sub-second, sub-cent USDC. The grant's own
  application committed to "Solana as the primary high-speed settlement layer."
- **Cheaper than bridging** — agents pay on the destination chain directly, no bridge fee/wait.
- **Matches the tranche-2 requirement** verbatim: "live MVP + some Solana integration."

## What already exists (verified, don't rebuild)
| Piece | Location | Status |
|-------|----------|--------|
| **Jupiter swap leg** | `gentech-treasury/scripts/gta_solana_leg.py` | ✅ LIVE quotes verified (SOL $1→0.0134, TAO $1→0.00505) |
| **Solana bridge adapter** | `10-Labs/AAE-Dry-Powder-Vault/agent/solana_bridge_adapter.py` | ✅ Across Base→Solana USDC |
| **solders + solana-py** | venv | ✅ installed |
| **Yield LP engine** | `gentech-treasury/scripts/yield_lp_engine.py` | ✅ Phase A |
| **Close executor** | `gentech-treasury/scripts/gta_close_executor.py` | ✅ Phase B |
| **Regime gate** | `gentech-treasury/scripts/regime_gate.py` | ✅ Phase C |
| **x402 gateway (multi-chain)** | `10-Labs/x402-gateway/server.py` | ✅ Base + Algorand rails |

## The MVP loop (Solana homebase)
```
Agent earns USDC via x402 (any chain)
        ↓
Bridge USDC → Solana (Across adapter, sub-5s)
        ↓
Treasury deploys USDC on Solana yield (Jupiter/routes)
        ↓
Regime gate decides: accumulate (yield) vs trade (SOL/TAO via Jupiter)
        ↓
Agent pays services from Solana wallet (sub-cent gas)
        ↓
Receipt logged (Q402 trust receipt pattern)
```

## What I'm building now (this session)
1. **Solana homebase orchestrator** — `solana_homebase.py`: ties bridge→deploy→yield→pay
   into one command (mirrors the venue-agnostic engine pattern). DRY_RUN by default.
2. **Verify the bridge adapter imports + quotes** cleanly (web3 present?).
3. **Wire the Solana leg into the treasury allocator** so SOL/TAO is a valid deployment target.
4. **Tranche-2 package** — a README + demo script that shows: live Solana quote → (bridged)
   → on-chain proof. This is the video + repo the grant reviewer sees.

## Funding needed to go LIVE (Jordan, from grant)
- Solana wallet gas: **~$2 SOL** (for Jupiter swaps)
- USDC to deploy: **~$20 USDC on Solana** (bridge from grant)
- Test end-to-end: SOL buy, TAO buy, receipt.

## $200 coding-subscription documentation (tranche-2 requirement)
The grant asks for coding subscription receipts totaling $200. Current stack (Jordan-confirmed Aug 7):
- VPS (always-online) **$43/mo**
- OpenCode Go **$10/mo**
- Ollama Cloud **$20/mo**
- Nous research sub **~$5-10/mo** (occasional)
- **Fixed monthly ≈ $73** (VPS + OpenCode + Ollama); with Nous ≈ $78-83/mo.
- **3 months of the fixed stack ≈ $219** — clears the $200 requirement. Document 3 months of VPS + OpenCode + Ollama receipts (or 2 months + Nous) to hit $200. Jordan to confirm which receipts we can upload.

## Repos for the submission
- `github.com/ProtoJay4789/solana-x402-mvp` (MVP)
- `github.com/ProtoJay4789/x402-gateway` (gateway)
- `github.com/ProtoJay4789/agent-economy-solana` (contracts)
- New: `github.com/ProtoJay4789/solana-homebase` (this orchestrator)
