# S11 Language Standard — SILENCE.OBJECTS

Version 1.1 | Adopted: 2026-01-01 | Status: ACTIVE

## Purpose

The S11 Language Standard defines the vocabulary requirements for all code,
documentation, and communications within the SILENCE.OBJECTS ecosystem.
Behavioral software must not medicalize, pathologize, or clinicalize human
patterns. Language shapes perception; this standard ensures SILENCE.OBJECTS
frames observation scientifically and ethically.

## Forbidden Terms

The following terms are FORBIDDEN in all source code, documentation,
comments, commit messages, and user-facing text:

| Forbidden | Reason | Use Instead |
|-----------|--------|-------------|
| disorder | Clinical framing | pattern, structural variant |
| symptom | Medical framing | signal, observation |
| diagnosis | Medical procedure | classification, analysis |
| patient | Clinical relationship | observer, participant |
| treatment | Medical intervention | intervention, protocol |
| illness | Pathological framing | structural variant |
| cure | Medical outcome | resolution, stabilization |
| therapy | Clinical service | structured observation |
| clinical | Medical context | observational, structured |
| dysfunction | Pathological labeling | divergence, atypical pattern |
| abnormal | Deficit framing | atypical, variant |
| medication | Medical substance | support protocol |

## Enforcement

1. **ESLint plugin** — `@silence/eslint-plugin` rule `no-pathologizing-terms`
2. **CI Sentinel** — `s11-sentinel.yml` workflow blocks PRs with violations
3. **Code review** — reviewers verify compliance before merge

## Exceptions

Terms may appear in:
- Legal/compliance documents quoting EU AI Act article text verbatim
- Test files explicitly testing that the terms are forbidden (use `// S11-ALLOWED`)
- CHANGELOG.md historical entries

## Rationale

### Ethical Foundation

Language is not neutral. In behavioral software, the vocabulary used to describe human patterns shapes how those patterns are perceived — by users, by contributors, and by the public. When software that observes behavioral patterns borrows vocabulary from clinical medicine, it implicitly frames human variation as deficiency. SILENCE.OBJECTS rejects this framing.

Human behavioral patterns are not deficits to be corrected. They are structures to be observed, understood, and worked with. The S11 Language Standard enforces this philosophical position at the level of every commit, every comment, and every user-facing string.

### Legal Risk Reduction

Clinical vocabulary in a non-medical product creates interpretive ambiguity. If SILENCE.OBJECTS documentation refers to users experiencing a "disorder" or receiving "treatment," a regulator might reasonably ask whether the product constitutes a medical device or health assessment tool under EU MDR, FDA 21 CFR, or equivalent national regulations.

The S11 Language Standard creates a clear, documented, and automatically enforced record that SILENCE.OBJECTS does not characterize its outputs in clinical terms. This record is publicly auditable in the git history of this repository.

### EU AI Act Positioning

The EU AI Act Annex III High Risk classification includes AI systems used in health contexts. The Limited Risk classification that PatternLens holds depends in part on the system not functioning as a health assessment tool. Consistent non-clinical language throughout all documentation reinforces this classification in any regulatory review.

### Ecosystem Consistency

SILENCE.OBJECTS spans multiple repositories, multiple contributors, and evolving documentation over a multi-year roadmap. Without automated enforcement, vocabulary drift is inevitable. The S11 Language Standard, enforced at CI level, guarantees consistency regardless of contributor familiarity with the standard.

## Approved Vocabulary Reference

| Domain | Non-S11 Alternative | S11-Compliant Term |
|---|---|---|
| Describing behavioral variation | disorder, dysfunction | pattern, structural variant, divergence |
| Describing observed signals | symptom | signal, observation, indicator |
| Describing analysis output | diagnosis | classification, analysis result |
| Describing the user relationship | patient | observer, participant, user |
| Describing interventions | treatment, therapy | protocol, structured observation, intervention |
| Describing statistical outliers | abnormal | atypical, variant, divergent |
| Describing health status | illness | structural variant (avoid health framing entirely) |
| Describing resolution | cure | resolution, stabilization |
| Describing supporting materials | medication | support protocol |

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2026-01-01 | Initial adoption |
| 1.1 | 2026-03-01 | Added approved vocabulary reference table; clarified exception scope |
