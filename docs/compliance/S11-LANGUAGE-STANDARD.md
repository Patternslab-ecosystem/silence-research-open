# S11 Language Standard — Summary

This document provides a summary of the S11 Language Standard and links to the full specification in `compliance/s11/`.

## What is S11

The S11 Language Standard forbids the use of pathologizing, medicalizing, or clinical vocabulary in all SILENCE.OBJECTS code, documentation, and communications. It is a mandatory engineering and community conduct standard.

## Key Documents

| Document | Description |
|---|---|
| [S11 Language Standard](../../compliance/s11/S11-LANGUAGE-STANDARD.md) | Full specification with forbidden terms, enforcement, rationale |
| [Forbidden Terms](../../compliance/s11/forbidden-terms.yaml) | Machine-readable list of all forbidden terms |
| [Approved Alternatives](../../compliance/s11/alternatives.yaml) | Machine-readable list of approved replacement terms |
| [ADR-003](../../governance/adr/ADR-003-s11-language.md) | Architecture Decision Record for S11 adoption |

## Quick Reference — Forbidden Terms

disorder, symptom, diagnosis, patient, treatment, illness, cure, therapy, clinical, dysfunction, abnormal, medication

## Enforcement

- **CI Sentinel** — `s11-sentinel.yml` workflow blocks any PR with violations
- **ESLint plugin** — `@silence/eslint-plugin` rule `no-pathologizing-terms`
- **Code review** — All reviewers verify S11 compliance

## Status

S11 Language Standard v1.1 is **ACTIVE** across all SILENCE.OBJECTS public repositories as of 2026-03-01.
