# Students — MAUTIC

**Project:** MAUTIC  
**Category:** MARKETING_TOOLS  
**Upstream:** https://github.com/mautic/mautic.git  
**Pinned commit:** `09b766402139924822b96db15364bfa4e36cc70b`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `5749d589e5fd9b46deacc43b9effc4335c18b2116a318f6ff9fa7d618e5c99d9`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `09b766402139924822b96db15364bfa4e36cc70b`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `5749d589e5fd9b46deacc43b9effc4335c18b2116a318f6ff9fa7d618e5c99d9`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
