# φ-Research Engine

## Overview

The φ-Research Engine is the systematic investigation framework for golden-ratio mathematical principles applied to behavioral observation systems. It operates within the SILENCE.OBJECTS ecosystem as the formal research layer — translating mathematical hypotheses into empirically testable propositions, collecting observation data through the SilenceEventV2 schema, and producing validated findings that inform the evolution of PatternLens.

## Core Hypothesis

The φ-Research Engine investigates a foundational proposition: **that structures organized according to golden-ratio (φ = 1.618...) proportions produce measurably different behavioral responses than structures organized according to arbitrary or uniform proportions.**

This proposition has precedent in visual perception research, architectural theory, and mathematical biology. The φ-Research Engine applies it specifically to the domain of digital behavioral observation — asking whether φ-proportioned spacing, timing, and rhythm reduce the cognitive effort required to sustain attentional focus during structured observation sessions.

## Methodology Summary

Research within the φ-Research Engine follows a structured protocol:

1. **Hypothesis formulation** — A specific, falsifiable proposition is stated with defined measurement criteria
2. **Protocol design** — Observation cohort size, session structure, and event collection parameters are specified
3. **Baseline establishment** — A pre-observation baseline measurement is collected
4. **Controlled observation** — Two cohorts (φ-proportioned vs. control condition) complete identical sessions
5. **SilenceEventV2 telemetry** — All events are collected using the Zero-PII schema
6. **PCS analysis** — `calculatePCS()` computes Pattern Compliance Scores; `trendVector()` classifies trajectory
7. **Statistical validation** — Significance testing at α = 0.05; effect size reported
8. **Finding publication** — Validated findings are published in `research/publications/`

Full methodology details are documented in `research/phi-research-engine/methodology.md`.

## Active Hypotheses

| ID | Title | Status | Opened |
|---|---|---|---|
| H01 | φ-Proportioned Spacing Reduces Attentional Friction | Active Investigation | 2026-Q1 |
| H02 | Fibonacci-Timed Breath Cycles Increase Flow State Frequency | Active Investigation | 2026-Q1 |

## Key Concepts

### Pattern Compliance Score (PCS)

PCS is the primary measurement output of PatternLens. It is a numerical score computed from SilenceEventV2 events collected during a session, reflecting the degree to which observed behavioral patterns align with φ-geometry-derived reference patterns. A higher PCS indicates closer alignment with φ-proportioned structures.

### trendVector

`trendVector()` classifies the trajectory of a session as ASCENDING, STABLE, or DESCENDING based on PCS progression over time. It is used as a secondary measurement in hypothesis analysis to capture directional trends beyond the session-level PCS value.

### φ-Spacing

φ-Spacing refers to the use of Fibonacci-sequence pixel values (8, 13, 21, 34, 55px) as the primary spacing scale in UI layouts. This is the independent variable in H01.

### Fibonacci Timing

Fibonacci timing refers to breath cycle durations following the proportional relationship of consecutive Fibonacci numbers (e.g., inhale 3000ms, hold 1854ms, exhale 4854ms ≈ φ × inhale). This is the independent variable in H02.

## How to Contribute Hypotheses

Researchers wishing to propose a new φ-Research Engine hypothesis should:

1. Open a GitHub Issue using the `research-proposal` template
2. State the hypothesis in falsifiable form: "If X, then Y, as measured by Z"
3. Specify the measurement protocol including cohort size and event types required
4. Reference relevant prior literature if applicable

Hypotheses are reviewed by Pattern and formally adopted via a governance motion before observation begins. Adopted hypotheses are added to the `hypotheses/` directory with a `H0N-` prefix and Active Investigation status.
