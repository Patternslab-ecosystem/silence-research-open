# ADR-001: PWA-First Architecture — Mobile Native Deferred to Phase 2

**ID:** ADR-001
**Status:** ACCEPTED
**Date:** 2026-01-15
**Deciders:** Pattern (Human Lead)
**Supersedes:** Internal Playbook ADR-009
**Technical Area:** Application Architecture

---

## Context

SILENCE.OBJECTS requires a front-end delivery strategy that balances reach, iteration velocity, and EU AI Act transparency obligations. Two primary options were evaluated:

1. **PWA-first** — A Progressive Web App delivered via browser, with optional native shell via Capacitor in a future phase.
2. **Native-first** — Separate iOS and Android applications with shared React Native or native Swift/Kotlin logic.

The product is in active development under Playbook v3. The core user interaction model (behavioral observation sessions, φ-breath guidance, Pattern Compliance Score display) does not require hardware APIs that are exclusive to native platforms at this stage.

Additionally, the EU AI Act Article 50 transparency obligation requires that users be clearly informed they are interacting with an AI system before their first interaction. The web context makes this disclosure technically straightforward, auditable, and testable in CI. Native app store distribution introduces additional release gates that could delay compliance implementation.

Internal Playbook ADR-009 established the original web-first preference; this ADR formalizes that decision in the public governance record.

## Decision

**Adopt PWA-first architecture.** Mobile-native delivery (Capacitor or React Native) is deferred to Phase 2, which begins no earlier than Playbook v4.

The following constraints apply immediately:

- `silence-experience-open` ships as a PWA only
- No Capacitor dependencies in any public repository
- Service Worker registration is required for offline baseline functionality
- The AIDisclosureBadge component must be rendered before any observation session begins
- Lighthouse PWA score target: ≥ 90

## Rationale

### Iteration Velocity

A single web codebase eliminates the platform divergence overhead of maintaining separate iOS and Android builds. Design iterations, compliance changes, and research instrumentation updates can ship continuously without app store review cycles.

### EU AI Act Compliance

Article 50 transparency disclosure is easier to implement, audit, and verify in a web context. The AIDisclosureBadge component can be tested in CI using Playwright or Cypress against a live build URL. Native app disclosure would require device-farm testing infrastructure not currently available.

### Single Codebase Advantage

TypeScript, React, and Tailwind are the shared language across the SILENCE.OBJECTS stack. A PWA requires no additional languages or build tooling beyond what already exists. Capacitor would introduce a Kotlin/Swift compilation step that currently has no specialist resource allocated.

### Research Instrumentation

SilenceEventV2 telemetry integration is significantly simpler in a browser context. Web Workers and browser APIs provide sufficient capability for all current φ-Research Engine measurement requirements.

### Ecosystem Positioning

Enterprise clients evaluating SILENCE.OBJECTS for integration typically begin with web-based proof-of-concept deployments. A high-quality PWA provides the best first impression for this audience without the friction of app store installation.

## Consequences

### Positive

- Faster delivery of Playbook v3 milestones
- Simplified CI/CD pipeline (single build target)
- EU AI Act Article 50 compliance implementable without additional infrastructure
- All research instrumentation available in web platform APIs
- Lighthouse score target is measurable in automated CI

### Negative / Trade-offs

- No access to native hardware APIs (push notifications with background delivery, biometric auth, deep ARKit/ARCore) until Phase 2
- Users on low-quality mobile browsers may experience degraded performance compared to a native app
- Phase 2 migration to Capacitor will require audit of all web-specific code patterns

### Constraints Introduced

- No Capacitor in `silence-experience-open` or any public repository
- Mobile-native features (biometric session unlock, background timers) are logged as Phase 2 items
- PWA manifest and service worker must be present and passing Lighthouse audit before any production release

## Review Date

This ADR is scheduled for review at Playbook v4 initiation, when Phase 2 mobile native feasibility will be reassessed.
