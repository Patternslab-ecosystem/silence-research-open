# Zero-PII Policy — SILENCE.OBJECTS

**Version:** 1.0
**Adopted:** 2026-01-15
**Status:** ACTIVE
**Legal Basis:** GDPR Article 25 (Data Protection by Design and by Default)

---

## 1. Purpose and Scope

This policy establishes the Zero-PII (Zero Personally Identifiable Information) requirement for all behavioral event data collected and processed within the SILENCE.OBJECTS ecosystem.

**Scope:** This policy applies to:

- All SilenceEventV2 behavioral event records
- All event schemas, TypeScript interfaces, and database table definitions
- All downstream consumers of behavioral event data
- All contributors to repositories that define or process event data

**Scope exclusion:** This policy does not apply to account management systems where user identity is required for service delivery (e.g., authentication). Those systems must be architecturally isolated from behavioral event data and are governed by a separate data processing policy.

---

## 2. Definition of PII

For the purposes of this policy, Personally Identifiable Information (PII) means any data element that, alone or in combination with other data, could be used to identify a natural person, including but not limited to:

- Full name, first name, last name, username
- Email address
- Phone number
- IP address (IPv4 or IPv6)
- Precise geolocation (latitude, longitude)
- Device identifier, advertising identifier, IDFA, GAID
- Browser fingerprint or user agent string with sufficient entropy to identify a device
- Cookie values linked to user identity
- Any government-issued identifier (national ID, passport number, tax ID)
- Any combination of indirect identifiers that could re-identify an individual

---

## 3. Prohibited Field Names

The following field names are PROHIBITED in any SilenceEventV2 payload, schema definition, database column, or derived dataset:

| Prohibited Field | Category |
|---|---|
| `email`, `e_mail` | Direct identifier |
| `userId`, `user_id`, `uid` | Direct identifier |
| `name`, `firstName`, `lastName`, `fullName` | Direct identifier |
| `phone`, `phoneNumber`, `telephone` | Direct identifier |
| `ip`, `ipAddress`, `ip_address`, `remoteIp` | Network identifier |
| `geolocation`, `location`, `lat`, `lon`, `latitude`, `longitude` | Location identifier |
| `deviceId`, `device_id`, `deviceFingerprint` | Device identifier |
| `adId`, `advertisingId`, `idfa`, `gaid` | Advertising identifier |
| `userAgent`, `user_agent`, `browser` | Device descriptor |
| `cookie`, `cookieId` | Session tracker |

The list above is non-exhaustive. The principle applies: if a field name suggests it might contain data that identifies a natural person, it is prohibited.

---

## 4. Permitted Identifier

The **only** permitted identifier in SilenceEventV2 payloads is `session_id`.

`session_id` requirements:
- Must be a UUID v4 generated client-side using a cryptographically secure random number generator
- Must be generated fresh for each observation session
- Must never be stored in association with any user account, email, or other identifier in any server-side system
- Must be treated as opaque — its only purpose is to correlate events within a single session

---

## 5. Technical Enforcement

### 5.1 isZeroPII() Validator

All SilenceEventV2 events must pass the `isZeroPII()` validation function before storage. This function:

- Checks all top-level keys against the prohibited field list
- Recursively checks nested objects
- Returns `false` and logs a violation if any prohibited field is detected
- Is implemented in `silence-core-open` as a published npm package function

### 5.2 Schema-Level Enforcement

TypeScript `interface SilenceEventV2` must not include any prohibited field names. The TypeScript compiler, combined with a linting rule, prevents prohibited fields from being added to the schema in CI.

### 5.3 CI PII Scan Workflow

A GitHub Actions workflow runs on every PR touching event schema files:

- Scans for prohibited field names using regex pattern matching
- Fails the PR if any prohibited field is detected in schema or migration files
- Produces a clear error message identifying the violating field

### 5.4 Supabase Row-Level Security

The Supabase event log table has row-level security policies that enforce:
- No columns matching prohibited field names may be added via migration
- All insertions are validated server-side

---

## 6. Data Flow

```
User Interaction
      │
      ▼
φ-Observation Engine (client-side)
      │  SilenceEventV2 { session_id (UUID), event_type, timestamp, phi_score }
      ▼
isZeroPII() Validation ──► FAIL → Event discarded, violation logged
      │ PASS
      ▼
Supabase Event Log (session_id only — no user identity)
      │
      ▼
Aggregate Metrics (cohort-level — individual records not exposed)
      │
      ▼
Benchmark 2030 / φ-Research Engine Analysis
```

No PII crosses any boundary in this data flow. The session UUID cannot be used to identify a natural person because no server-side system links it to user identity.

---

## 7. Audit Mechanism

### Regular Audits

- CI PII scan runs on every PR
- Quarterly manual audit of Supabase schema to verify no prohibited columns exist
- Annual GDPR compliance review includes Zero-PII policy audit

### Incident Response

If a PII field is found in event data:
1. Immediate escalation to Pattern
2. Suspension of event ingestion
3. Scope assessment of affected records
4. Purge of affected records with documented justification
5. Root cause analysis and CI rule update
6. Incident report published in this repository

---

## 8. Legal Basis and References

- **GDPR Article 25** — Data protection by design and by default
- **GDPR Recital 78** — Technical and organisational measures for data minimisation
- **ADR-002** — Zero-PII Event Schema Design (governance decision record)
- **SilenceEventV2 schema** — Published in silence-core-open
