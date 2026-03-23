# ADR-003: S11 Language Standard Adoption

**ID:** ADR-003
**Status:** ACCEPTED
**Date:** 2026-01-01
**Deciders:** Pattern (Human Lead)
**Technical Area:** Engineering Standards, Ethics, Legal Risk

---

## Context

SILENCE.OBJECTS is a behavioral pattern observation system. Its core function — observing and analyzing human behavioral patterns — is adjacent to fields that have historically used clinical and medical language to describe human cognitive and behavioral variation.

As the codebase, documentation, and user-facing content grew during Playbook v1, a pattern emerged: developers and contributors naturally reached for clinical vocabulary when describing behavioral observations. Terms such as "disorder," "symptom," "diagnosis," and "treatment" appeared in code comments, variable names, and documentation drafts.

This is a significant problem on multiple dimensions:

**Ethical:** Clinical language medicalizes human behavioral variation. SILENCE.OBJECTS does not assess, diagnose, or intervene in human health. Framing behavioral patterns using medical vocabulary implies a clinical relationship and assessment authority that the product does not have and should not claim.

**Legal:** In the EU and UK, products that function as medical devices or diagnostic tools are subject to separate regulatory regimes (MDR, UKCA, FDA 510(k)). Using clinical terminology in product documentation creates interpretive ambiguity that could draw regulatory scrutiny. The EU AI Act Annex III High Risk classification includes AI systems used in health and safety contexts. A clear non-clinical language standard reduces the risk of SILENCE.OBJECTS being misclassified as a High Risk system.

**Product Integrity:** If SILENCE.OBJECTS frames behavioral observation in clinical terms, it implies a therapeutic or diagnostic capability it does not possess. This is misleading to users and creates product liability exposure.

## Decision

**Adopt the S11 Language Standard v1.1 as a mandatory engineering and documentation standard across the entire SILENCE.OBJECTS ecosystem.**

The following terms are FORBIDDEN in all source code, documentation, comments, commit messages, API field names, and user-facing text:

| Forbidden Term | Required Alternative |
|---|---|
| disorder | pattern, structural variant |
| symptom | signal, observation |
| diagnosis | classification, analysis |
| patient | observer, participant |
| treatment | intervention, protocol |
| illness | structural variant |
| cure | resolution, stabilization |
| therapy | structured observation |
| clinical | observational, structured |
| dysfunction | divergence, atypical pattern |
| abnormal | atypical, variant |
| medication | support protocol |

Enforcement mechanisms:

1. **ESLint plugin** — `@silence/eslint-plugin` rule `no-pathologizing-terms` runs in CI on all TypeScript/JavaScript files
2. **CI Sentinel** — `s11-sentinel.yml` GitHub Actions workflow blocks any PR where forbidden terms appear in markdown or YAML files
3. **Code review** — All reviewers are expected to flag S11 violations before approval

### Permitted Exceptions

The following contexts may contain forbidden terms without triggering a violation:

- Legal and compliance documents that quote EU AI Act, GDPR, or other regulatory text verbatim (the regulation itself uses this vocabulary)
- Test files explicitly testing that the S11 sentinel correctly detects forbidden terms (must include `// S11-ALLOWED` comment)
- The S11 specification documents themselves (forbidden-terms.yaml, S11-LANGUAGE-STANDARD.md) where terms appear in the "forbidden" column of definition tables

## Rationale

### Ethical Positioning

Behavioral software that describes human patterns without clinical framing respects the autonomy and dignity of the people being observed. SILENCE.OBJECTS observes patterns; it does not assess deficits. The language standard enforces this distinction consistently across every artifact the organization produces.

### Legal Risk Reduction

Clear, consistent non-clinical language creates a defensible record that SILENCE.OBJECTS is not a medical device, diagnostic tool, or health assessment system. This record is auditable in the public git history of this repository. In any regulatory inquiry, the S11 Language Standard and its enforcement history demonstrate proactive, systematic effort to avoid clinical framing.

### EU AI Act Risk Classification

The Limited Risk classification confirmed in `compliance/eu-ai-act/risk-classification.md` depends in part on SILENCE.OBJECTS not functioning as a health, employment, credit, or law enforcement decision-making system. Consistent use of non-clinical language across all documentation reinforces this classification and reduces the risk of reclassification.

### Developer Experience

Providing approved alternatives removes ambiguity for contributors. When a developer wants to describe a behavioral pattern and is uncertain which term to use, the S11 standard provides clear, pre-approved vocabulary that is both accurate and compliant.

## Consequences

### Positive

- Clear ethical positioning against medicalization of behavioral variation
- Reduced legal risk of medical device regulatory misclassification
- Stronger EU AI Act Limited Risk classification evidence
- Consistent product language across code, docs, and user-facing content
- CI enforcement means violations are caught before merge, not in production

### Negative / Trade-offs

- Onboarding friction for contributors who are unfamiliar with the standard — addressed by comprehensive documentation and clear CI error messages
- Some precision may be lost in technical descriptions where clinical vocabulary would be the most precise available term — the approved alternatives are adequate for SILENCE.OBJECTS use cases

### Technical Constraints

- ESLint plugin `@silence/eslint-plugin` must be present in all public repositories
- `s11-sentinel.yml` workflow must run on all PRs to public repositories
- All new contributors must review `compliance/s11/S11-LANGUAGE-STANDARD.md` before first commit

## Review Date

This ADR is reviewed annually. The forbidden terms list may be expanded but not reduced without a new ADR superseding this one.
