# Data Flow Map — SILENCE.OBJECTS Behavioral Event Data

**Version:** 1.0
**Last Updated:** 2026-03-23
**GDPR Basis:** Article 25 — Data Protection by Design

---

## Overview

This document maps all data flows within the SILENCE.OBJECTS behavioral event pipeline. It demonstrates that no personally identifiable information crosses any system boundary at any stage of the data flow.

---

## Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│  USER DEVICE (Browser / PWA)                                    │
│                                                                 │
│  1. User initiates observation session                          │
│     └─► session_id = crypto.randomUUID()  [UUID v4, local]     │
│          │                                                      │
│          │  NO USER IDENTITY LINKED TO session_id               │
│          ▼                                                      │
│  2. φ-Observation Engine captures interactions                  │
│     └─► SilenceEventV2 {                                        │
│            session_id,   ← opaque UUID only                     │
│            event_type,   ← enum value                           │
│            timestamp,    ← Unix ms                              │
│            phi_score,    ← computed number                      │
│            trend_vector  ← ASCENDING|STABLE|DESCENDING          │
│         }                                                       │
│          │                                                      │
│          ▼                                                      │
│  3. isZeroPII() validation (client-side)                        │
│     ├─► FAIL → Event DISCARDED, violation logged locally        │
│     └─► PASS → Continue                                         │
│          │                                                      │
│          ▼                                                      │
│  4. calculatePCS() — Pattern Compliance Score computed          │
│     └─► PCS displayed to user in session UI                     │
└──────────────────┬──────────────────────────────────────────────┘
                   │
                   │  HTTPS transport (TLS 1.3)
                   │  Payload: SilenceEventV2 (Zero PII)
                   │  No session-to-user mapping transmitted
                   ▼
┌─────────────────────────────────────────────────────────────────┐
│  SUPABASE EVENT LOG (Server-side)                               │
│                                                                 │
│  5. Server-side isZeroPII() validation                          │
│     ├─► FAIL → Insert REJECTED, 400 error returned              │
│     └─► PASS → Record inserted                                  │
│                                                                 │
│  6. Event record stored:                                        │
│     ┌─────────────────────────────────────┐                     │
│     │ id          | UUID (auto)           │                     │
│     │ session_id  | UUID (from client)    │  ← ONLY IDENTIFIER  │
│     │ event_type  | text                  │                     │
│     │ timestamp   | bigint                │                     │
│     │ phi_score   | numeric               │                     │
│     │ trend_vector| text                  │                     │
│     └─────────────────────────────────────┘                     │
│     NO PII COLUMNS EXIST IN THIS TABLE                          │
│                                                                 │
│  7. Row-Level Security (RLS)                                    │
│     └─► No user identity queries permitted                      │
└──────────────────┬──────────────────────────────────────────────┘
                   │
                   │  SQL aggregation only
                   │  No individual records exposed downstream
                   ▼
┌─────────────────────────────────────────────────────────────────┐
│  AGGREGATED METRICS PIPELINE                                    │
│                                                                 │
│  8. Cohort-level aggregation                                    │
│     └─► SELECT AVG(phi_score), COUNT(*), event_type             │
│          GROUP BY event_type, DATE(timestamp)                   │
│     └─► Individual session_id values NOT present in output      │
│                                                                 │
│  9. Benchmark 2030 metrics export                               │
│     └─► Aggregate numbers only (no session-level data)          │
│                                                                 │
│  10. φ-Research Engine hypothesis analysis                      │
│      └─► Cohort comparison using aggregate PCS distributions    │
│          No individual re-identification possible                │
└─────────────────────────────────────────────────────────────────┘
```

---

## PII Boundary Verification

| Boundary | Data Crossing | PII Present? | Verification |
|---|---|---|---|
| User device → Supabase | SilenceEventV2 payload | No | isZeroPII() client + server |
| Supabase → Metrics pipeline | SQL aggregate query results | No | No session_id in GROUP BY output |
| Metrics pipeline → Reports | Aggregate numbers | No | No individual records in reports |
| Any system → External | None (no external data sharing) | N/A | No third-party data sharing |

---

## Authentication System Isolation

SILENCE.OBJECTS uses Supabase Auth for user account management. The authentication system is **architecturally isolated** from the behavioral event pipeline:

- Auth tables (`auth.users`) are in a separate Supabase schema from event tables
- No foreign key relationship exists between `auth.users` and the event log table
- No application code performs a JOIN between user identity and behavioral events
- Service role access to auth tables is restricted to authenticated session management only

This isolation means that even if the event log were fully public, no user could be identified from its contents.

---

## Data Retention

| Data Type | Retention Period | Rationale |
|---|---|---|
| SilenceEventV2 events | 24 months from session date | Research analysis window |
| Aggregate metrics | Indefinite | Benchmark 2030 trend analysis |
| session_id values | 24 months (with events) | Required for session-level aggregation |
| User auth data | Duration of account + 30 days | Account management |

session_id values have no value after the retention period as they cannot be linked to natural persons.

---

## References

- **Zero-PII Policy:** `compliance/gdpr/zero-pii-policy.md`
- **ADR-002:** `governance/adr/ADR-002-zero-pii.md`
- **GDPR Article 25:** Data protection by design and by default
- **GDPR Article 5(1)(c):** Data minimisation principle
