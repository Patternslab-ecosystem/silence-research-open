# ADR-001: Three-Tier Public Repository Structure

**ID:** ADR-001 (docs)
**Status:** ACCEPTED
**Date:** 2026-01-15
**Deciders:** Pattern (Human Lead)
**Technical Area:** Repository Architecture, Open Source Strategy
**Related Motion:** MOTION-001

---

## Context

The SILENCE.OBJECTS project must balance open-source transparency with protection of proprietary application logic and production infrastructure. A clear public/private repository boundary is needed to:

- Enable public auditability of compliance documentation (required for EU AI Act Article 13 voluntary compliance)
- Enable open-source package publishing for ecosystem adoption
- Protect production infrastructure configuration and proprietary algorithms

Various options were considered:
- **Single public monorepo** — Maximum transparency but exposes all proprietary code
- **Fully private** — Maximum protection but zero community trust or regulatory auditability
- **Two-tier** — One public docs repo, one private app repo — insufficient separation of concerns
- **Three-tier** — Separate repos for packages, experience, and governance — maps to distinct audiences

## Decision

**Adopt a three-tier public repository structure:**

| Repository | Content | Audience | License |
|---|---|---|---|
| `silence-core-open` | npm packages, event schemas, utilities | Developers, integrators | MIT |
| `silence-experience-open` | PWA product showcase | Designers, enterprise evaluators | MIT |
| `silence-research-open` | Governance, compliance, research | Regulators, researchers, partners | MIT |

Private repositories retain proprietary application logic (CORE) and production infrastructure (Silence-Experience private).

## Rationale

**Audience separation:** Each public repository serves a distinct primary audience. Mixing governance docs with application code reduces usability for both developers and regulators.

**Compliance auditability:** A dedicated governance repository makes it unambiguous where to find compliance documentation. Regulators do not need to navigate application code to find the EU AI Act risk classification.

**Package publishing independence:** `silence-core-open` can publish to npm independently of the governance repository's release cadence. Coupling them would introduce unnecessary coordination overhead.

**Enterprise evaluation:** `silence-experience-open` provides a clean, code-focused repository that enterprise evaluators can review without governance overhead.

## Consequences

- Three separate GitHub repositories under `Patternslab-ecosystem`
- CI must pass independently on each repository
- Cross-repository references use full URLs, not relative paths
- Former single public repo structure is deprecated
- MOTION-001 formally adopts this decision at the governance level
