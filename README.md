<div align="center">

# silence-research-open

**SILENCE.OBJECTS governance hub — Benchmark 2030 · EU AI Act compliance · φ-Research Engine**

[![CI](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/ci.yml/badge.svg)](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/ci.yml)
[![S11 Sentinel](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/s11-sentinel.yml/badge.svg)](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/s11-sentinel.yml)
[![Security](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/security.yml/badge.svg)](https://github.com/Patternslab-ecosystem/silence-research-open/actions/workflows/security.yml)
[![EU AI Act: Limited Risk](https://img.shields.io/badge/EU%20AI%20Act-Limited%20Risk-blue)](compliance/eu-ai-act/risk-classification.md)
[![GDPR: Zero PII](https://img.shields.io/badge/GDPR-Zero%20PII-green)](compliance/gdpr/zero-pii-policy.md)
[![S11: Active](https://img.shields.io/badge/S11-Active-orange)](compliance/s11/S11-LANGUAGE-STANDARD.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Benchmark 2030](https://img.shields.io/badge/Benchmark-2030-purple)](benchmark-2030/README.md)

</div>

---

## Overview

`silence-research-open` is the public governance, compliance, and research hub for the [SILENCE.OBJECTS](https://github.com/Patternslab-ecosystem) behavioral observation ecosystem. It is the canonical source of truth for every strategic decision, regulatory obligation, and research hypothesis that shapes how SILENCE.OBJECTS is built, governed, and operated. Every document in this repository is version-controlled, PR-reviewed, and publicly auditable — by design.

This repository exists at the intersection of three imperatives: regulatory transparency, research integrity, and governance accountability. As the EU AI Act moves toward full enforcement in August 2026, organizations operating AI systems must demonstrate not only that they have identified their obligations, but that they have documented, implemented, and monitored compliance systematically. This repository is that demonstration — a living, versioned compliance record that any regulator, partner, or auditor can inspect at any commit in the repository's history.

The intended audience for `silence-research-open` is broad and deliberate. Regulators and compliance teams will find the EU AI Act risk classification, Article 50 transparency implementation evidence, and GDPR Zero-PII data flow maps. Academic researchers and behavioral scientists will find the φ-Research Engine methodology, active hypotheses, and the publication pipeline. Enterprise partners and integrators evaluating SILENCE.OBJECTS for procurement will find the governance motions, ADRs, and Benchmark 2030 quality targets that define the project's commitments and trajectory. Open-source contributors will find the contributing guide, code of conduct, and clear pathways to propose ADRs, compliance updates, and research hypotheses.

## Features

- **Complete EU AI Act compliance documentation** — Risk classification (Limited Risk confirmed), Article 50 transparency obligations, Article 11 technical documentation, and a milestone timeline with 2 August 2026 enforcement tracking
- **GDPR Zero-PII architecture** — Full policy documentation, ASCII data flow map, and technical enforcement specification for the `isZeroPII()` validator
- **S11 Language Standard** — Machine-readable forbidden terms list, approved alternatives, and CI enforcement via the S11 sentinel workflow
- **Governance motions** — Formal, numbered records of strategic decisions (MOTION-001: Open-Source Repository Strategy — ADOPTED)
- **Architecture Decision Records** — ADR-001 (PWA-first), ADR-002 (Zero-PII schema), ADR-003 (S11 adoption) with full context, rationale, and consequences
- **Benchmark 2030** — YAML-defined quality targets across four dimensions with quarterly progress reports and dashboard generation infrastructure
- **φ-Research Engine** — Systematic investigation framework for golden-ratio principles in behavioral observation, with active hypotheses H01 and H02
- **GitHub-native CI/CD** — Markdown linting, S11 sentinel, Trivy security scan, Release Please, Renovate, and Dependabot all configured and active

## Repository Structure

```
silence-research-open/
├── governance/
│   ├── command-center/     # Command Center methodology and authority model
│   ├── motions/            # Governance motions (MOTION-NNN.md)
│   └── adr/                # Architecture Decision Records (ADR-NNN-slug.md)
│
├── compliance/
│   ├── eu-ai-act/          # Risk classification, Art. 50, Art. 11, timeline
│   ├── gdpr/               # Zero-PII policy, data flow map
│   └── s11/                # S11 Language Standard, forbidden-terms.yaml, alternatives.yaml
│
├── benchmark-2030/
│   ├── targets.yaml        # Machine-readable quality targets
│   ├── quarterly/          # Quarterly progress reports (Q1-2026.md, ...)
│   └── dashboards/         # Dashboard generation documentation
│
├── research/
│   ├── phi-research-engine/
│   │   ├── methodology.md  # Observation protocol and statistical standards
│   │   └── hypotheses/     # H01, H02 and future hypotheses
│   └── publications/       # Publication pipeline tracking
│
├── docs/
│   ├── ARCHITECTURE.md     # Repository structure and conventions
│   ├── CONTRIBUTING.md     # How to propose ADRs, docs, hypotheses
│   ├── CODE_OF_CONDUCT.md  # Contributor Covenant 2.1 + S11 addendum
│   └── SECURITY.md         # Security policy and PII incident response
│
└── .github/
    ├── workflows/           # CI, S11 sentinel, security, release
    └── ISSUE_TEMPLATE/      # Structured issue forms
```

## Compliance Status

| Regulation | Obligation | Status |
|---|---|---|
| EU AI Act | Risk Classification | **LIMITED RISK — Confirmed** |
| EU AI Act | Article 5 — No prohibited practices | **Compliant** |
| EU AI Act | Article 50 — User disclosure | **Compliant** (AIDisclosureBadge) |
| EU AI Act | Article 13 — Technical documentation | **Compliant** (voluntary) |
| GDPR | Article 25 — Privacy by design | **Compliant** (Zero-PII architecture) |
| GDPR | Article 5(1)(c) — Data minimisation | **Compliant** |
| S11 | Language Standard v1.1 | **Active — CI enforced** |

**Enforcement deadline:** EU AI Act Limited Risk obligations are enforceable from **2 August 2026.**

Full documentation: [`compliance/eu-ai-act/`](compliance/eu-ai-act/) · [`compliance/gdpr/`](compliance/gdpr/) · [`compliance/s11/`](compliance/s11/)

## Benchmark 2030

Benchmark 2030 defines quantitative quality and governance targets for the SILENCE.OBJECTS ecosystem through 2030, with quarterly progress reviews.

| Dimension | Key Target | Status |
|---|---|---|
| Technical Quality | Test coverage ≥ 80%, Lighthouse ≥ 90 | In Progress |
| Compliance | Zero S11 violations, Art. 50 implemented | Met |
| Research Output | ≥ 2 active hypotheses, 3 publications by 2030 | H01 + H02 active |
| Ecosystem Growth | 3 public repos, 5 npm packages | 3 repos live, 5 packages published |

Machine-readable targets: [`benchmark-2030/targets.yaml`](benchmark-2030/targets.yaml)
Q1 2026 report: [`benchmark-2030/quarterly/Q1-2026.md`](benchmark-2030/quarterly/Q1-2026.md)

## φ-Research Engine

The φ-Research Engine investigates whether golden-ratio mathematical principles produce measurably different behavioral outcomes in digital observation contexts.

**Core question:** Do φ-proportioned structures (spacing, timing, rhythm) reduce cognitive friction during structured behavioral observation sessions, as measured by Pattern Compliance Score?

**Active Hypotheses:**

| ID | Hypothesis | Status |
|---|---|---|
| H01 | φ-proportioned spacing (8/13/21/34/55px) reduces attentional friction vs. uniform 8px grid | Active Investigation |
| H02 | Fibonacci-timed breath cycles (3000/1854/4854ms) increase flow state frequency vs. equal-duration cycles | Active Investigation |

Methodology: [`research/phi-research-engine/methodology.md`](research/phi-research-engine/methodology.md)
Hypotheses: [`research/phi-research-engine/hypotheses/`](research/phi-research-engine/hypotheses/)
Publications pipeline: [`research/publications/`](research/publications/)

## Documentation

| Document | Description |
|---|---|
| [Command Center](governance/command-center/README.md) | Governance methodology, decision authority, sprint structure |
| [MOTION-001](governance/motions/MOTION-001.md) | Open-Source Repository Strategy — ADOPTED |
| [ADR-001: PWA-First](governance/adr/ADR-001-pwa-first.md) | PWA architecture decision, mobile native deferred |
| [ADR-002: Zero-PII](governance/adr/ADR-002-zero-pii.md) | Zero-PII event schema decision |
| [ADR-003: S11](governance/adr/ADR-003-s11-language.md) | S11 Language Standard adoption |
| [EU AI Act Risk Classification](compliance/eu-ai-act/risk-classification.md) | Full Annex III analysis — Limited Risk confirmed |
| [Zero-PII Policy](compliance/gdpr/zero-pii-policy.md) | GDPR Article 25 implementation |
| [S11 Language Standard](compliance/s11/S11-LANGUAGE-STANDARD.md) | Forbidden terms, enforcement, rationale |
| [Architecture](docs/ARCHITECTURE.md) | Repository structure and conventions |
| [Contributing](docs/CONTRIBUTING.md) | How to contribute ADRs, docs, hypotheses |

## Ecosystem

SILENCE.OBJECTS is organized across three public repositories:

| Repository | Contents | Audience |
|---|---|---|
| [silence-core-open](https://github.com/Patternslab-ecosystem/silence-core-open) | npm packages, SilenceEventV2 schema, utilities | Developers, integrators |
| [silence-experience-open](https://github.com/Patternslab-ecosystem/silence-experience-open) | PWA product showcase, AIDisclosureBadge | Designers, enterprise evaluators |
| **silence-research-open** (this repo) | Governance, compliance, research | Regulators, researchers, partners |

## Contributing

Contributions are welcome for ADR proposals, compliance document corrections, research hypothesis proposals, and documentation improvements.

All contributions must comply with the [S11 Language Standard](compliance/s11/S11-LANGUAGE-STANDARD.md) and pass CI validation. See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for the full process.

## License

[MIT](LICENSE) — Copyright © 2026 Patternslab-ecosystem
