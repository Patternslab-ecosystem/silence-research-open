# Contributing to silence-research-open

Thank you for your interest in contributing to the SILENCE.OBJECTS governance and compliance documentation. This guide explains how to propose changes, what standards apply, and how the review process works.

## What This Repository Accepts

This is a documentation-only repository. Contributions should be one of:

- **ADR proposals** — New Architecture Decision Records for significant decisions
- **Compliance document updates** — Corrections or additions to regulatory compliance documentation
- **Research proposals** — New φ-Research Engine hypothesis proposals
- **Factual corrections** — Fixing incorrect information with supporting references
- **Broken link fixes** — Correcting dead or outdated links
- **Governance motion proposals** — Formal proposals for Pattern consideration

**This repository does not accept contributions that:**
- Add application code (belongs in silence-core-open or silence-experience-open)
- Modify the S11 forbidden terms list without a superseding ADR
- Change compliance classifications without supporting regulatory analysis
- Use S11-forbidden terms (see `compliance/s11/S11-LANGUAGE-STANDARD.md`)

## S11 Language Standard

Every contribution must comply with the S11 Language Standard. Before submitting a PR, verify your text contains none of the following terms: disorder, symptom, diagnosis, patient, treatment, illness, cure, therapy, clinical, dysfunction, abnormal, medication.

The CI sentinel will block any PR containing these terms. See `compliance/s11/S11-LANGUAGE-STANDARD.md` for approved alternatives.

## Proposing a New ADR

1. Open a GitHub Issue using the **Documentation Request** template, selecting "New ADR"
2. Describe the decision, its context, and your proposed resolution
3. Wait for Pattern review and acknowledgement before writing the full ADR
4. Once acknowledged, fork the repository and create `governance/adr/ADR-NNN-slug.md`
5. Use the ADR format: **ID, Status, Date, Deciders, Context, Decision, Rationale, Consequences**
6. Open a PR referencing the original issue
7. Address review comments and await Pattern approval

## Proposing a Compliance Document Update

Compliance documents (in `compliance/`) carry regulatory weight. Updates must:
- Cite the specific regulatory article being addressed
- Reference authoritative primary sources (EU AI Act text, GDPR text, etc.)
- Not weaken any compliance position without explicit Pattern approval

For minor corrections (typos, broken links), a PR without a prior issue is acceptable.
For substantive changes, open an issue first.

## Proposing a Research Hypothesis

1. Open a GitHub Issue using the **Documentation Request** template, selecting "Research hypothesis proposal"
2. State the hypothesis in falsifiable form: "If X, then Y, as measured by Z"
3. Specify the measurement protocol: cohort size, session structure, event types, statistical test
4. Reference `research/phi-research-engine/methodology.md` to confirm alignment with established protocol
5. Pattern will review and, if adopted, open a governance motion to activate the hypothesis
6. Upon motion adoption, a new `H0N-slug.md` file is created in `research/phi-research-engine/hypotheses/`

## PR Standards

- PRs must include all items in the pull request template checklist
- PR titles should follow conventional commit format: `feat: add ADR-004 typescript strict mode`, `fix: correct article reference in risk-classification`
- One logical change per PR where possible
- All CI checks must pass before merge

## Review Process

All PRs require review by Pattern (`@Patternslab-ecosystem`). The CODEOWNERS file reflects this. Review typically takes 2–5 business days. If a PR has been open for more than 7 days without review, a comment on the PR requesting status is appropriate.

## Code of Conduct

All contributors must follow the `docs/CODE_OF_CONDUCT.md`. The S11 Language Standard is considered part of the community conduct standard for this project.
