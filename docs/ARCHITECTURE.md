# Repository Architecture

## Overview

`silence-research-open` is the governance, compliance, and research hub for the SILENCE.OBJECTS ecosystem. It is a documentation-first repository — no application code is shipped from this repo. Its purpose is to provide a publicly auditable, version-controlled record of governance decisions, regulatory compliance, and research methodology.

## Directory Structure

```
silence-research-open/
├── .github/                      # GitHub automation and templates
│   ├── workflows/                # CI/CD workflows
│   │   ├── ci.yml                # Main CI: markdown lint + S11 sentinel
│   │   ├── s11-sentinel.yml      # Standalone S11 language check for PRs
│   │   ├── security.yml          # Trivy security scan
│   │   └── release.yml           # Release Please automation
│   ├── ISSUE_TEMPLATE/           # Structured issue forms
│   ├── CODEOWNERS                # Review assignment
│   ├── FUNDING.yml               # Sponsorship configuration
│   ├── dependabot.yml            # Dependency update automation
│   └── pull_request_template.md  # PR checklist
│
├── governance/                   # Formal governance documents
│   ├── command-center/           # Command Center methodology
│   ├── motions/                  # Governance motions (MOTION-NNN.md)
│   └── adr/                      # Architecture Decision Records (ADR-NNN.md)
│
├── compliance/                   # Regulatory compliance documentation
│   ├── eu-ai-act/                # EU AI Act obligations and analysis
│   ├── gdpr/                     # GDPR data protection documentation
│   └── s11/                      # S11 Language Standard specification
│
├── benchmark-2030/               # Quality targets and quarterly reports
│   ├── targets.yaml              # Machine-readable benchmark targets
│   ├── quarterly/                # Quarterly progress reports
│   └── dashboards/               # Dashboard generation documentation
│
├── research/                     # φ-Research Engine
│   ├── phi-research-engine/      # Methodology and active hypotheses
│   │   └── hypotheses/           # Individual hypothesis files (H0N-*.md)
│   └── publications/             # Publication pipeline tracking
│
├── docs/                         # Developer-facing documentation
│   ├── ARCHITECTURE.md           # This file
│   ├── CONTRIBUTING.md           # Contribution guide
│   ├── CODE_OF_CONDUCT.md        # Community standards
│   ├── SECURITY.md               # Security policy
│   ├── ADR/                      # Docs-level ADRs
│   └── compliance/               # Compliance summaries
│
├── README.md                     # Repository overview
├── CHANGELOG.md                  # Version history
├── LICENSE                       # MIT license
├── package.json                  # Minimal package descriptor
├── renovate.json                 # Dependency update configuration
├── .markdownlint.json            # Markdown lint rules
├── .editorconfig                 # Editor formatting standards
├── .nvmrc                        # Node.js version specification
└── .gitignore                    # Git exclusion patterns
```

## Document Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Governance motions | `MOTION-NNN.md` | `MOTION-001.md` |
| Architecture Decision Records | `ADR-NNN-slug.md` | `ADR-001-pwa-first.md` |
| Hypothesis files | `H0N-slug.md` | `H01-phi-spacing-attention.md` |
| Quarterly reports | `QN-YYYY.md` | `Q1-2026.md` |
| Published findings | `PUB-H0N-slug.md` | `PUB-H01-phi-spacing-result.md` |

## Governance Hierarchy

```
Pattern (Human Lead)
      │
      ├── Governance Motions (governance/motions/)
      │         Formal decisions adopted by Pattern
      │
      ├── Architecture Decision Records (governance/adr/)
      │         Technical decisions with context, rationale, consequences
      │
      ├── Compliance Documentation (compliance/)
      │         Regulatory obligation analysis and evidence
      │
      └── Research (research/)
                  Hypothesis formulation, methodology, publications
```

## CI Architecture

The CI pipeline enforces two non-negotiable quality gates on every PR:

1. **Markdown lint** — All `.md` files must pass markdownlint rules defined in `.markdownlint.json`
2. **S11 sentinel** — No forbidden terms (per `compliance/s11/forbidden-terms.yaml`) may appear in any changed file

Both gates must pass before a PR can be merged.
