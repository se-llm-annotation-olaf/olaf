---
layout: default
title: OLAF Example
---

# OLAF Examples

- [Example 1: Code Comment Annotation](#task-code-comment-annotation)
- [Example 2: Novice Programmers' Emotion in Text](#task-novice-programmers-emotion)

# Task: Code Comment Annotation

Annotate source code comments to identify the **software engineering intent** expressed in each comment.

Each comment must receive **exactly one label** describing its primary purpose.


Use the following label set:

- **Implementation**: The comment explains how code works or why code was implemented in a specific way.

- **Bug Fix**: The comment documents a defect, workaround, or corrective change.

- **Enhancement**: The comment describes an improvement, refactoring, or optimization.

- **Testing**: The comment relates to test cases, test logic, or validation behavior.

- **Documentation**: The comment provides descriptive or explanatory information for readers.

- **Indeterminate**: The intent cannot be reliably inferred from the comment alone.

## How to Do It

### Step 0: Data Collection

- Collect **10,000 source code comments** from software repositories.
- Each comment is stored with minimal context (file path, language, commit ID).
- No labels are assigned at this stage.

### Step 1: Define the Unit of Annotation

- Each **single code comment** is one annotation unit.
- Inline and block comments are treated equally.
- Surrounding code is used only when necessary to interpret intent.

### Step 2: Initial Human Annotation

1. Randomly sample **400 code comments** from the collected set.
2. Assign **two human annotators**.
3. Provide written definitions and examples for each label.
4. Annotators independently label all 400 comments.
5. Measure inter-annotator agreement using Cohen’s κ.
6. Resolve disagreements and finalize the annotation guidelines.

This step establishes the **reference interpretation of the task**.

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

### Step 4: Scaling Annotation

1. Apply both LLMs to the remaining **unlabeled comments** from the original 10,000.
2. Treat each LLM as an independent annotator.
3. Aggregate labels using:
   - Majority voting when LLMs agree, or
   - Probabilistic aggregation when LLMs disagree
4. Assign one final label per comment.

This enables annotation at scale while preserving measurement consistency.

### Step 5: Transparency

Document:
- Label definitions
- Annotation instructions
- Prompt template
- Model identifiers and parameters
- Human-human agreement
- Human-LLM agreement
- Aggregation method


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



# Task: Novice Programmers' Emotion

Filter a large collection of online discussion posts to retain only those that are **relevant for manual annotation**, based on predefined criteria.

The goal is to **reduce manual labour during annotation** while preserving recall for relevant instances.


## Filtering Objective

Retain posts that satisfy **both** conditions:

1. Written by **novice programmers**
2. Contain **non-neutral emotional expressions related to learning**

Posts that do not meet both conditions are excluded from further analysis.

---

## How to Do It

### Step 1: Initial Data Collection

- Collect a large, raw dataset of posts from online programming communities.
- No labels are assigned at this stage.
- Expect the majority of posts to be irrelevant for the target analysis.


### Step 2: Define Filter Criteria

Formulate binary filter questions:

- **Q1:** Does the post exhibit any learning-related emotion (e.g., confusion, frustration, curiosity)?
- **Q2:** Is the post written by a novice or beginner programmer?

A post must satisfy **both** conditions to pass the filter.


### Step 3: LLM-Based Filtering

1. Select one/more LLM to act as a **filter**, not an annotator.
2. Use a fixed prompt with:
   - Explicit definitions of emotions
   - Clear indicators of novice status
   - Yes/No answers only
3. Apply the LLM to every post in the raw dataset.
4. Retain only posts where the LLMs answers **Yes** to both Q1 and Q2.

At this stage, the LLM is used **only to reduce the dataset**, not to generate labels.

### Step 4: Human Verification

1. Randomly sample posts that passed the filter.
2. Have human reviewers verify:
   - Emotional relevance
   - Novice authenticity
3. Remove false positives identified by humans.

This step bounds **filtering error** and mitigates LLM hallucination.

### Step 5: Selection for Annotation

1. From the verified filtered set, randomly sample posts for manual annotation.
2. Exclude all posts filtered out in earlier steps.
3. Proceed with full annotation only on the retained subset.

This ensures that manual effort is spent **only on high-signal data**.

## Reliability and Transparency

Report:
- Filtering prompt
- Model version and parameters
- Acceptance criteria
- Human verification procedure
- Proportion of data retained and discarded

The filter is treated as a **measurement instrument**, not ground truth.

## Output

- Filtered dataset
- Human-verified subset
- Filtering prompt and configuration
- Retention statistics
