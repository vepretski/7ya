# 7YA.io production recovery receipt — 2026-09-04

> **STATUS: RECOVERY RECEIPT ONLY — NOT A DEPLOYABLE OR COMPLETE SOURCE EXPORT.**
>
> Do not merge or deploy this branch as a replacement for production until a complete AppDeploy snapshot export has been recovered and compared.

## Observed production truth

- Canonical public hostnames: `7ya.io`, `www.7ya.io`
- Both hostnames were observed `active` in AppDeploy custom-domain state on 2026-09-04.
- Current runtime: AppDeploy app `697a008fddc309b142`.
- Current applied AppDeploy version at this receipt: **v93 / `1788537766940`**, created 2026-09-04 19:02:46 Asia/Jerusalem.
- Immediate rollback: **v92 / `1788537321639`**, created 2026-09-04 18:55:21 Asia/Jerusalem.
- The remote AppDeploy source snapshot is the current source-of-runtime. It contains the full React/Vite + backend application, canonical corpus/evidence layers, multilingual routes, 100 Moments/life layers, media/archive systems, Bro Chat, QA tooling and production assets.
- AppDeploy terminal QA after v93 reported 0 frontend errors, 0 backend errors and 0 network errors and generated fresh mobile/desktop screenshots.
- AppDeploy did **not** report an E2E run for the current version (`e2e_tests = null`). Therefore E2E PASS must not be claimed from this receipt.

## NVIDIA / Bro Chat truth rule

Production provider order remains:

`NVIDIA Nemotron -> AppDeploy tool-agent -> local deterministic fallback`

Configured NVIDIA model in the recovered runtime is `nvidia/nemotron-3-super-120b-a12b`.

Two production truth fixes were applied on 2026-09-04:

1. The Bro Chat UI no longer displays `NVIDIA NIM · connected` merely because an NVIDIA credential is configured. It displays NVIDIA only after the returned answer identifies its actual provider as NVIDIA.
2. Backend status/agent semantics now distinguish **configured** from **observed execution**. Privacy-safe provider observations store only provider, model, release and timestamp after a real Bro Chat reply; they do not store the user's question or answer content for this purpose.

A secret name or configuration flag is never execution proof.

## Source-control findings

The following repositories were inspected and must **not** be treated as the current production source without a new comparison:

- `vepretski/7ya.io` — repository root is an OpenCode monorepo, although later 7YA routes/commits were layered into it. Its historical Vercel deployment is not the current AppDeploy source snapshot.
- `7guard-io/7ya.io` — contains substantial 7YA material but is heavily contaminated by the `generative-ai-for-beginners` course corpus and historical overlays.
- `vepretski/7ya-os` — Expo/React Native application template, not the current web runtime.
- `7guard-io/igorvepretski` — older Lovable/Vite prototype; current AppDeploy structures such as `DocumentaryHome` were not found.
- GitLab candidates are older independent projects/mirrors and are not established as current production source.

## Hosting lineage findings

A Vercel team/project named `7ya.io` exists and is linked to `vepretski/7ya.io`; its observed production history is older than the current AppDeploy runtime. **Do not redeploy that repository over 7ya.io.**

Netlify/Replit instances are secondary/historical candidates unless later evidence proves otherwise.

## Current lineage

```text
7ya.io + www.7ya.io
        ↓
AppDeploy custom-domain routing
        ↓
app 697a008fddc309b142
        ↓
v93 / 1788537766940
        ↓
remote AppDeploy source snapshot
```

## Export status

The AppDeploy connector currently exposes versioned source reads/globs but no single full-repository/archive export action. The live snapshot contains 400+ source/config/public files plus binary assets. A partial copy would create another false source of truth, so **no partial root replacement was performed**.

Until a byte-complete export is made and verified, the AppDeploy remote snapshot remains the authoritative source-of-runtime and this branch remains only a recovery ledger/guardrail.

## Anti-overwrite gate

Before any future production cutover from GitHub/GitLab/Vercel/Netlify/Replit:

1. Recover the complete AppDeploy snapshot.
2. Compare it against the proposed repository.
3. Preserve all production-only behavior and assets.
4. Run build/type/test gates.
5. Exercise Bro Chat and verify the returned provider rather than credential presence.
6. Inspect mobile and desktop renders.
7. Confirm public `7ya.io` release identity after deployment.

**If any of those steps is missing, do not overwrite AppDeploy production.**
