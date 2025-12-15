---
layout: default
title: OLAF Example
---

# OLAF Example: Code Comment Annotation

## Task

Annotate source code comments to identify the **software engineering intent** expressed in each comment.

Each comment must receive **exactly one label** describing its primary purpose.

---

## Annotation Dimension: Comment Intent

Use the following label set:

- **Implementation**: The comment explains how code works or why code was implemented in a specific way.

- **Bug Fix**: The comment documents a defect, workaround, or corrective change.

- **Enhancement**: The comment describes an improvement, refactoring, or optimization.

- **Testing**: The comment relates to test cases, test logic, or validation behavior.

- **Documentation**: The comment provides descriptive or explanatory information for readers.

- **Indeterminate**: The intent cannot be reliably inferred from the comment alone.

---

## How to Do It

### Step 0: Data Collection

- Collect **10,000 source code comments** from software repositories.
- Each comment is stored with minimal context (file path, language, commit ID).
- No labels are assigned at this stage.

---

### Step 1: Define the Unit of Annotation

- Each **single code comment** is one annotation unit.
- Inline and block comments are treated equally.
- Surrounding code is used only when necessary to interpret intent.

---

### Step 2: Initial Human Annotation

1. Randomly sample **400 code comments** from the collected set.
2. Assign **two human annotators**.
3. Provide written definitions and examples for each label.
4. Annotators independently label all 400 comments.
5. Measure inter-annotator agreement using Cohen’s κ.
6. Resolve disagreements and finalize the annotation guidelines.

This step establishes the **reference interpretation of the task**.

---

### Step 3: LLM Annotation and Human–Model Agreement

Use **two independent LLMs as annotators**:

- `gpt-oss:20b`
- `mistral-small-3.2:24b`

Procedure:

1. Fix all inference parameters:
   - Model version
   - Temperature
   - Prompt template
2. Apply both LLMs to the **same 400 comments** annotated by humans.
3. Require exactly one label per comment.
4. Allow the label **Indeterminate** when intent is unclear.
5. Compute:
   - Agreement between each LLM and human annotators
   - Agreement between the two LLMs

If agreement with humans is **substantial**, proceed to scaling.

---

### Step 4: Scaling Annotation

1. Apply both LLMs to the remaining **unlabeled comments** from the original 10,000.
2. Treat each LLM as an independent annotator.
3. Aggregate labels using:
   - Majority voting when LLMs agree, or
   - Probabilistic aggregation when LLMs disagree
4. Assign one final label per comment.

This enables annotation at scale while preserving measurement consistency.

---

### Step 5: Transparency

Document:
- Label definitions
- Annotation instructions
- Prompt template
- Model identifiers and parameters
- Human-human agreement
- Human-LLM agreement
- Aggregation method

---

### Step 6: Drift Monitoring

1. Retain the original 400-comment calibration set.
2. Re-run LLM annotation when:
   - A model version changes/new model is used
   - Prompt wording changes
3. Compare agreement against the calibration set.
4. Recalibrate if agreement drops below the predefined threshold.

---

## Output

- Annotated code comments
- Annotation guidelines
- Human-human agreement
- Human-LLM agreement
- Aggregated labels
