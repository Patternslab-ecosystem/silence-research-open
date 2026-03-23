# φ-Research Engine — Publications

## Overview

This directory tracks the publication pipeline for findings from the φ-Research Engine. Publications represent the culmination of the full research cycle: hypothesis formulation → controlled observation → statistical analysis → peer review → publication.

## Publication Process

### Stage 1: Hypothesis Activation

A hypothesis is formally activated when it is committed to `research/phi-research-engine/hypotheses/` with Active Investigation status. The commit timestamp serves as the pre-registration date, establishing that the measurement protocol was defined before data collection.

### Stage 2: Data Collection

Observation data is collected per the protocol defined in the hypothesis file. The observation period is considered complete when the minimum cohort size defined by the power analysis is reached.

### Stage 3: Analysis

Statistical analysis is conducted per `research/phi-research-engine/methodology.md`. Results, including null results, are fully documented.

### Stage 4: Internal Review

Pattern reviews the analysis. If the methodology was followed correctly and the statistics are sound, the finding advances to the draft publication stage.

### Stage 5: Draft Publication

A draft manuscript is committed to this directory as `DRAFT-H0N-[short-title].md`. The draft is opened for community comment via GitHub Discussion.

### Stage 6: External Review

For findings intended for academic publication, the manuscript is submitted to a peer-reviewed venue. The submission record is documented here.

### Stage 7: Publication

Upon acceptance (or upon decision to self-publish as a technical report), the final publication is committed as `PUB-H0N-[short-title].md` and a DOI or permanent URL is recorded.

## Current Pipeline Status

| Hypothesis | Stage | Notes |
|---|---|---|
| H01 — φ-Spacing Attention | Stage 1 (Activated) | Cohort recruitment pending |
| H02 — Fibonacci Timing Flow | Stage 1 (Activated) | Protocol review pending |

## Target: 3 Publications by 2030

The Benchmark 2030 target defines 3 publications by end of the 2026–2030 period. The current pipeline has 2 active hypotheses. Additional hypotheses will be proposed and activated as H01 and H02 advance through the pipeline.

## Publication Venues

The φ-Research Engine targets the following publication channels:

- **Technical reports** — self-published in this repository with permanent GitHub URL
- **Open access preprints** — arXiv (cs.HC or q-bio.NC) for findings with broader academic relevance
- **Peer-reviewed venues** — Human-Computer Interaction, Frontiers in Neuroscience (Cognitive Science section), or equivalent, for findings that meet the statistical and methodological standards required for peer review

All publications use the Zero-PII constraint: no individual participant data appears in any publication. Only cohort-level aggregates are reported.
