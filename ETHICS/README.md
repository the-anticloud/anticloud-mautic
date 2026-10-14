# Ethics — MAUTIC

**Project:** MAUTIC  
**Category:** MARKETING_TOOLS  
**Upstream:** https://github.com/mautic/mautic.git  
**Pinned commit:** `09b766402139924822b96db15364bfa4e36cc70b`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `5749d589e5fd9b46deacc43b9effc4335c18b2116a318f6ff9fa7d618e5c99d9`  
**Date:** October 2026

## Position

MAUTIC is packaged for offline deployment with a verifiable audit trail. The
ethical questions this raises are answered by making the system's behaviour
checkable rather than by policy statements.

## The four commitments

1. **No hidden egress.** The deployment has no external API dependency; this is
   testable by running it with the network disconnected.
2. **Attributable output.** Every artifact is recorded in a hash chain, so what
   the system produced can be reconstructed.
3. **Operator control.** The institution owns the hardware and the keys.
4. **Refusal to overclaim.** Where a certification is not held, the project says
   so rather than implying it.

## Dual use

This project is packaged for civilian and public-sector deployment. Where an
upstream has dual-use characteristics, the licence gate and the reference-only
marking in `BENCH.json` record that.
