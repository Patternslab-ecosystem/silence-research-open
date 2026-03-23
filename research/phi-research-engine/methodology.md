# φ-Research Engine — Methodology

**Version:** 1.0
**Status:** Active
**Maintained by:** Patternslab-ecosystem

---

## 1. Observation Protocol

### 1.1 Session Structure

All φ-Research Engine observations are conducted within structured SILENCE.OBJECTS sessions. A standard session consists of:

- **Pre-session calibration** (60 seconds): Participant completes a standardized orientation sequence to establish baseline attentional state
- **Main observation window** (5 minutes): The primary measurement period during which the independent variable (φ-proportioned or control condition) is active
- **Post-session rating** (optional): Participant rates perceived focus quality on a 1–5 scale

Sessions are conducted through the silence-experience-open PWA. Participants are assigned to conditions using a random cohort assignment mechanism that does not expose condition assignment to the application layer during the session.

### 1.2 Cohort Assignment

- Cohorts are balanced by session count and day-of-week to control for temporal confounds
- Neither the participant nor the application UI reveals which condition is active during the session
- Condition assignment is stored separately from session event data and merged only during analysis

### 1.3 Participant Eligibility

- Adults (18+) engaging voluntarily with SILENCE.OBJECTS
- No minimum prior exposure required for H01 and H02
- Repeat participants are tracked by session count, not identity (Zero-PII constraint applies)

---

## 2. Data Collection — SilenceEventV2

All observations are captured using the SilenceEventV2 event schema. Relevant event types for φ-Research Engine hypotheses:

| Event Type | Description | Used in |
|---|---|---|
| `SESSION_START` | Session initiated | H01, H02 |
| `SESSION_END` | Session completed | H01, H02 |
| `ATTENTION_SHIFT` | Attentional disruption detected | H01 |
| `FLOW_STATE` | Sustained attentional engagement detected | H01, H02 |
| `BREATH_CYCLE` | Breath cycle event (inhale/hold/exhale phase) | H02 |
| `PCS_COMPUTED` | Pattern Compliance Score computed for window | H01, H02 |

All events conform to the Zero-PII policy. No participant-identifying information is present in any payload.

---

## 3. Analysis Pipeline

### 3.1 calculatePCS()

`calculatePCS()` is the primary analysis function. It accepts a sequence of SilenceEventV2 events for a session and returns a Pattern Compliance Score between 0 and 1.

The scoring algorithm:

1. Extracts φ-score values from each event
2. Computes a weighted rolling average using φ-proportioned window sizes (8, 13, 21 events)
3. Applies a φ-alignment coefficient based on the ratio of FLOW_STATE to ATTENTION_SHIFT events
4. Returns the normalized composite score

### 3.2 trendVector()

`trendVector()` accepts a sequence of PCS values over a session and returns the trajectory classification:

- `ASCENDING`: PCS slope > +0.05 per minute
- `STABLE`: PCS slope between -0.05 and +0.05 per minute
- `DESCENDING`: PCS slope < -0.05 per minute

### 3.3 Cohort Aggregation

For hypothesis testing, individual session PCS values are aggregated by cohort:

1. Retrieve all sessions in the observation period for each cohort
2. Compute mean PCS and standard deviation per cohort
3. Compute FLOW_STATE frequency (events per session) per cohort

---

## 4. Statistical Validity Requirements

### 4.1 Minimum Cohort Size

Power analysis is required before each hypothesis observation period. Minimum requirements:

- Two-tailed t-test, α = 0.05, power = 0.80
- Estimated effect size from pilot data or prior literature
- Minimum n = 30 per cohort for exploratory hypotheses without prior effect size estimate

### 4.2 Significance Testing

- Primary test: two-sample independent t-test (H01, PCS difference between cohorts)
- Secondary test: χ² test of independence (H02, FLOW_STATE frequency distribution)
- Bonferroni correction applied when testing multiple endpoints within one hypothesis

### 4.3 Effect Size

Effect size is reported for all significant and non-significant results:
- Cohen's d for continuous outcomes (PCS)
- Cramér's V for categorical outcomes (flow state frequency)

### 4.4 Pre-Registration

Hypothesis protocols are pre-registered in the GitHub repository (hypothesis file committed) before data collection begins. Post-hoc modification of measurement criteria is not permitted without opening a new hypothesis ID.

---

## 5. Publication Criteria

A finding is eligible for publication when:

1. Observation period is complete and cohort minimum n is met
2. Statistical analysis is complete with effect sizes reported
3. Pre-registered protocol was followed without material modification
4. Results reviewed by Pattern
5. No S11 Language Standard violations in the publication text

Findings that do not reach statistical significance are published as null results. The φ-Research Engine maintains a policy of full publication regardless of outcome direction.

---

## 6. Research Ethics

All φ-Research Engine observations follow the principles of voluntary participation, transparency of purpose, and Zero-PII data collection. No deception is used in study design. Participants are informed via the AIDisclosureBadge that an AI observation system is active during their session.

The observation protocol for H01 and H02 does not meet the threshold for formal IRB review under most national frameworks (no medical risk, no vulnerable populations, full Zero-PII data, voluntary participation). However, Pattern reserves the right to request an independent ethics review for any hypothesis that involves novel intervention types or expanded participant populations.
