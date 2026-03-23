# MOTION-001: Public Open-Source Repository Strategy

**Status:** ADOPTED
**Date:** 2026-03-23
**Author:** Pattern (Human Lead)
**Approved by:** Pattern

## Context

The SILENCE.OBJECTS ecosystem requires a clear strategy for open-source publication to attract research partners, enterprise clients, and the global developer community while protecting proprietary application code.

## Decision

Adopt a three-tier repository architecture:

1. **silence-core-open** — open-source packages (MIT)
2. **silence-experience-open** — product showcase PWA (MIT)
3. **silence-research-open** — governance and compliance hub (MIT)

Private repositories (CORE, Silence-Experience) retain proprietary application logic and production infrastructure configurations.

## Rationale

- Open-source packages build ecosystem trust and developer adoption
- Compliance documentation must be publicly auditable for EU AI Act obligations
- Governance transparency differentiates SILENCE.OBJECTS from closed-source behavioral products

## Consequences

- All three repos are PUBLIC under MIT license
- Former public repos (RESEARCH, BUSINESS, Silence-Experience) are migrated to private
- CI must pass on all three public repos before marking Playbook v3.0 complete
