# Educators — MAUTIC

**Project:** MAUTIC  
**Category:** MARKETING_TOOLS  
**Upstream:** https://github.com/mautic/mautic.git  
**Pinned commit:** `09b766402139924822b96db15364bfa4e36cc70b`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `5749d589e5fd9b46deacc43b9effc4335c18b2116a318f6ff9fa7d618e5c99d9`  
**Date:** October 2026

## Teaching with MAUTIC

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `5749d589e5fd9b46deacc43b9effc4335c18b2116a318f6ff9fa7d618e5c99d9` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.
