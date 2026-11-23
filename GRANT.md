# Tranche-2 submission — what to run, and what it proves

**Grant:** Superteam Earn — Agentic Engineering (Tranche 2, second 100 USDG)
**Requirement:** a live, working MVP with Solana integration, plus ~$200 of coding-subscription receipts.

## One command a reviewer can run

```
git clone https://github.com/Gentech-Labs/solana-homebase
cd solana-homebase
python3 tranche2_demo.py --fast
```

**No wallet, no API key, no dependency install.** The quote path is stdlib-only by design — a reviewer
with a bare Python gets live Jupiter prices or an honest `INCOMPLETE`.

Expected on a working run:

```
## 2. Live settlement quotes (Jupiter, real)
  - SOL: $5 USDC -> <N> SOL
  - TAO: $5 USDC -> <N> TAO
# ✅ Demo complete — every quote above came back from Jupiter in this run.
```

Exit code `0` means every quote returned. **Exit `2` means at least one failed and nothing above
should be read as verified** — that exit code is the deliverable's integrity, not ceremony.

## What each piece is, honestly

| Piece | State |
|---|---|
| Jupiter quote rail (SOL / TAO) | ✅ **live, verified 2026-11-23** |
| Jupiter swap execution | ⏸ code complete, **needs a funded keypair** — never executed against real funds |
| Across bridge Base→Solana | 🟡 quote path only; recipient is `pending` until a wallet is funded |
| Regime-gated allocation plan | 🟡 deterministic plan output; not wired to an allocator that moves money |
| x402 gateways paid from Solana | ✅ gateway live on Base; **Solana rail offered in the 402, not yet settled** |

**I am naming the unfunded pieces rather than describing them as done.** A grant reviewer who finds a
green tick over an unexecuted path closes the application; one who sees an honest table can fund the
step that is actually missing.

## The Solana integration, stated precisely

The treasury does not just "support Solana" — it treats Solana as the **settlement homebase**:

```
agent earns USDC via x402 (Base today)
  → bridge to Solana (Across, sub-5s, ~0.08%)
  → deploy on Solana (Jupiter, USDC)
  → pay services from the Solana wallet
  → receipt per payment
```

**Solana's advantage in that loop is arithmetic, not sentiment:** sub-cent fees mean a single API call
can be its own payment, which is the premise of x402 and the reason the rail matters at all.

## Funding needed to go fully live

- **~$2 SOL** for gas on the swap legs
- **~$20 USDC on Solana** to deploy and prove the loop on-chain

Everything else is built. What is missing is the transaction, not the code.
