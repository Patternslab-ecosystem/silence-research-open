# ADR-002: Zero-PII Event Schema Design

**ID:** ADR-002
**Status:** ACCEPTED
**Date:** 2026-01-15
**Deciders:** Pattern (Human Lead)
**Technical Area:** Data Architecture, Privacy Engineering

---

## Context

SILENCE.OBJECTS collects behavioral observation data during user sessions. This data is used to compute the Pattern Compliance Score (PCS), validate φ-Research Engine hypotheses, and generate aggregated metrics for Benchmark 2030 reporting.

A fundamental design decision must be made: should behavioral event payloads contain any form of user identification, or should the schema be architected to be structurally incapable of carrying personally identifiable information?

The EU General Data Protection Regulation (GDPR) Article 25 establishes the principle of data protection by design and by default. GDPR Article 9 imposes heightened restrictions on special category data, which could plausibly encompass behavioral health observations. SILENCE.OBJECTS operates in a space adjacent to behavioral science; any link between event data and identifiable individuals would significantly expand the regulatory compliance surface.

The alternative — a Zero-PII schema — eliminates the regulatory risk entirely by making it technically impossible to link behavioral events to natural persons at the schema level.

## Decision

**Adopt Zero-PII event schema design for all SilenceEventV2 payloads.**

The following constraints are mandated:

- `session_id` is the only identifier permitted in event payloads
- `session_id` must be an opaque UUID v4 generated client-side
- `session_id` must never be linked to any user identity in any server-side system
- The following field names are PROHIBITED in any event payload: `email`, `userId`, `user_id`, `name`, `firstName`, `lastName`, `phone`, `ip`, `ipAddress`, `ip_address`, `geolocation`, `lat`, `lon`, `latitude`, `longitude`, `deviceId`, `device_id`, `fingerprint`, `userAgent`, `user_agent`
- The `isZeroPII()` validator function must be run on every event before storage
- CI PII scan workflow must verify no prohibited field names appear in schema definitions

## Rationale

### GDPR Article 25 — Privacy by Design

Article 25 requires data controllers to implement technical measures that ensure data protection principles are met by default. A schema that structurally cannot carry PII is the strongest possible implementation of this requirement. It eliminates the risk of accidental PII collection through developer error or feature creep.

### Reduced Compliance Surface

If behavioral events cannot be linked to individuals, SILENCE.OBJECTS is not a personal data processor for the purposes of those events. This eliminates GDPR Article 13/14 notification obligations for event data, removes the need for a Data Processing Agreement for event storage providers, and simplifies the Data Protection Impact Assessment.

### Open-Source Schema Safety

The Zero-PII constraint enables the SilenceEventV2 schema to be published in the public `silence-research-open` repository without privacy risk. Researchers, enterprise evaluators, and compliance auditors can inspect the complete schema without any redaction.

### Research Integrity

φ-Research Engine hypotheses are tested on cohort-level aggregate patterns, not individual user behavior. The Zero-PII constraint aligns the data architecture with the research methodology: cohort results are what matter, not individual records.

### Trust Differentiation

In the behavioral software market, PII-free data collection is a significant trust differentiator. It can be disclosed openly in compliance documentation, marketing materials, and regulatory submissions.

## Consequences

### Positive

- Full GDPR Article 25 compliance by design
- SilenceEventV2 schema publishable in open-source repository
- No Data Processing Agreement required for event storage
- Simplified Data Protection Impact Assessment
- Research cohort analysis is unaffected (cohort aggregation does not require individual identity)

### Negative / Trade-offs

- Personalized features (returning user experience, personal PCS history) require a separate, explicitly opted-in identity layer that is architecturally isolated from event data
- A/B testing at individual level is not possible without the separate identity layer
- Debugging specific user-reported issues requires session ID correlation, which must be managed through a separate, access-controlled system

### Technical Constraints

- `isZeroPII()` validation function is mandatory in the event ingestion path
- Any field addition to SilenceEventV2 must be reviewed against the prohibited field list
- Downstream consumers of event data must document that they will not add PII fields
- CI PII scan must run on every PR touching event schema files

## Review Date

This ADR is reviewed annually or when a new data collection requirement is proposed that may require user identification.
