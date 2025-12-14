
---

## 3. `index.md` (GitHub Pages Home)

```markdown
---
layout: default
title: OLAF Framework
---

# OLAF Framework

## Overview
Large Language Models are increasingly used to annotate software engineering artifacts such as issues, commits, and qualitative data. Despite their growing adoption, methodological rigor, reproducibility, and reliability are often insufficiently addressed.

OLAF introduces a structured operationalization framework that treats LLM-based annotation as a measurement process rather than an automation shortcut.

## Motivation
Current LLM-based annotation practices often suffer from:
- Missing configuration and prompt details
- Lack of reliability and calibration reporting
- Sensitivity to prompt and model variation
- Limited reproducibility across studies

OLAF addresses these gaps by defining explicit, measurable constructs.

## Core Dimensions
OLAF is organized around six dimensions:

### 1. Reliability
Measures agreement among annotators using chance-corrected statistics such as Cohen’s kappa and Krippendorff’s alpha.

### 2. Consensus
Captures group-level agreement and task ambiguity using correlation-based measures.

### 3. Aggregation
Combines multiple annotators through majority voting or probabilistic models such as Dawid-Skene, GLAD, or MACE.

### 4. Transparency
Ensures reproducibility through full disclosure of model versions, prompts, parameters, and annotation settings.

### 5. Calibration
Evaluates whether model confidence scores correspond to empirical accuracy using metrics such as Expected Calibration Error and Brier Score.

### 6. Drift
Quantifies annotation stability under prompt, configuration, or model changes using metrics such as Jensen-Shannon Divergence or agreement deltas.

## Annotation Configurations
OLAF supports multiple annotation workflows:
- Human-in-the-Loop
- Model-in-the-Loop
- Verifier-in-the-Loop
- LLM-as-a-Filter
- LLM-as-a-Judge
- LLM-as-an-Annotator

Each configuration implies different risks, benefits, and reporting requirements.

## Guidelines
OLAF recommends that empirical studies:
1. Explicitly declare the annotation configuration
2. Fully document model and prompt details
3. Report reliability and aggregation methods
4. Track calibration and drift over time
5. Treat LLM outputs as measurements requiring validation

## Limitations
OLAF assumes constrained stability of LLMs and acknowledges limitations posed by opaque proprietary models and stochastic decoding. Metrics bound observable variability rather than guaranteeing deterministic behavior.

## Reference
If you use OLAF, please cite the paper.
