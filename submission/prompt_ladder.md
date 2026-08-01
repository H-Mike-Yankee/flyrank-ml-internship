# Prompt Engineering Ladder

## Track
AI/ML Project Communication — Generating a technical project summary for hiring managers

## Goal
The purpose of this exercise was to improve a weak prompt step-by-step, adding exactly one layer at a time, and comparing outputs at each stage to see what each layer actually fixes — and what it doesn't.

---

# Baseline Prompt

**Prompt:**
> Write about my project.

**Generated output:**
> I recently worked on an exciting project that showcases the power of data-driven innovation. Using cutting-edge technology, I developed a solution that transforms raw information into actionable insights, driving impactful results and unlocking new possibilities. This project demonstrates strong technical skills and a passion for solving real-world problems through smart, scalable solutions.

**What changed:** Nothing yet — this is the unmodified starting point.

**What improved:** N/A.

**What failed:** Zero real content. No dataset, no model, no metric — the output could describe any project. Full of buzzwords ("cutting-edge," "unlocking new possibilities") with nothing behind them.

**Next step:** Give the model an actual goal instead of an open-ended instruction.

---

# Version 1 — Clearer Goal

**Layer added:** Clearer goal

**Prompt:**
> Write a summary explaining what I built in my ML project and what problem it solves.

**Generated output:**
> I built a machine learning project focused on solving a real business problem. The project identifies patterns in data to help teams make smarter decisions faster. By leveraging modern ML techniques, I created a solution that improves efficiency and provides valuable insights that would be difficult to obtain manually.

**Analysis:**
- **What changed in the prompt:** Added a specific goal (explain what was built and what problem it solves) instead of a vague "write about."
- **What improved in output:** Slightly more directional — now at least framed around problem-solving via ML.
- **What still failed:** Still no specifics — no dataset, no model name, no number. "Leveraging modern ML techniques" is a buzzword with no content behind it.
- **What to try next:** The model has no idea who is reading this, so it defaults to generic language. Audience needs to be specified next.

---

# Version 2 — Defined Audience

**Layer added:** Audience

**Context:** Target reader is an AI/ML hiring manager.

**Prompt:**
> Write a summary explaining what I built in my ML project and what problem it solves, for an AI/ML hiring manager evaluating internship candidates.

**Generated output:**
> As part of my machine learning work, I built a solution designed to help organizations prioritize where to focus their efforts. Using a trained model, I was able to identify high-value opportunities more effectively than traditional rule-based methods. This project reflects strong applied ML skills and a results-driven approach that would bring immediate value to any engineering team.

**Analysis:**
- **What changed in the prompt:** Specified the reader as an AI/ML hiring manager evaluating internship candidates.
- **What improved in output:** Tone shifted toward what a hiring manager would expect — more outcome-oriented, less like a personal reflection.
- **What still failed:** Still fabricating confidence ("immediate value," "results-driven approach") with no facts behind it. No real model name, dataset size, or number. Audience alone changes tone, not truth.
- **What to try next:** The model needs actual facts, or it will keep inventing generic but hollow claims to fill the gap.

---

# Version 3 — Real Context

**Layer added:** Project context

**Verified facts used:**
- FlyRank ML Internship
- Lane 2: Refresh / Content Opportunity Scoring
- 30,000-page dataset
- Pipeline stages: `01_prepare_features → 02_baseline_score → 03_train_model → 04_evaluate_and_export → 05_build_pdf_report`
- Models: Logistic Regression, Decision Tree, Random Forest
- Metric: Precision@50
- Random Forest: 0.74 Precision@50
- Baseline: 0.24 Precision@50

**Prompt:**
> Write a summary for an AI/ML hiring manager explaining what I built. Context: I worked on the FlyRank ML Internship's Content Refresh Prioritization project (Lane 2: Refresh / Content Opportunity Scoring). I ran the starter pipeline (01_prepare_features → 02_baseline_score → 03_train_model → 04_evaluate_and_export → 05_build_pdf_report) on a 30,000-page dataset. I tested Logistic Regression, Decision Tree, and Random Forest models, evaluated with Precision@50. Random Forest reached 0.74 Precision@50 in this evaluation setup, versus 0.24 for the baseline rule.

**Generated output:**
> During the FlyRank ML Internship, I worked on the Content Refresh Prioritization project in Lane 2 (Refresh / Content Opportunity Scoring). I ran the starter pipeline — from feature preparation through model training and evaluation — on a 30,000-page dataset, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, a substantial improvement over the 0.24 achieved by the baseline rule-based approach. This result highlights the value of applying machine learning to prioritization problems that traditional rules struggle to capture.

**Analysis:**
- **What changed in the prompt:** Added real, verified project facts instead of leaving the model to guess.
- **What improved in output:** Now it is actually describing this project — real numbers, real model names, real metric, real pipeline stages. Usable content, not filler.
- **What still failed:** "Highlights the value of applying machine learning" and "substantial improvement" drift toward an unearned confident-summary tone. No sentence count or format constraint, so length and framing are whatever the model chose.
- **What to try next:** Lock down format so the output doesn't drift into a tone the project can't back up yet.

---

# Version 4 — Output Format

**Layer added:** Specified output format

**Requirement:** Exactly two sentences — (1) problem and approach, (2) result.

**Prompt:**
> Write a summary for an AI/ML hiring manager explaining what I built. Context: I worked on the FlyRank ML Internship's Content Refresh Prioritization project (Lane 2). I ran the starter pipeline on a 30,000-page dataset, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, versus 0.24 for the baseline rule. Write exactly two sentences: one stating the problem and approach, one stating the result.

**Generated output:**
> I built a pipeline to prioritize which of 30,000 pages a content team should review first, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, compared to 0.24 for the baseline rule.

**Analysis:**
- **What changed in the prompt:** Specified an exact structure — two sentences, one for problem/approach, one for result.
- **What improved in output:** Tight, exactly two sentences, no fluff, no unearned confidence language. Close to a usable final pitch.
- **What still failed:** Accurate, but doesn't scope that this was a training exercise on a starter dataset, not a production result. Read alone, it could be mistaken for a finished, deployed system.
- **What to try next:** Add explicit constraints against overclaiming so the model doesn't need a human to catch drift after the fact.

---

# Version 5 — Constraints

**Layer added:** Constraints

**Constraints added:**
- Direct technical language
- No buzzwords
- No production claims
- No unsupported success claims
- Avoid words like: innovative, cutting-edge, revolutionize, leverage

**Prompt:**
> Write a summary for an AI/ML hiring manager explaining what I built. Context: I worked on the FlyRank ML Internship's Content Refresh Prioritization project (Lane 2). I ran the starter pipeline on a 30,000-page dataset, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, versus 0.24 for the baseline rule. Write exactly two sentences: one stating the problem and approach, one stating the result. Voice: direct, technical, no buzzwords. Do not claim production readiness or results beyond what was measured. Do not use words like "innovative," "cutting-edge," "revolutionize," or "leverage."

**Generated output:**
> As part of the FlyRank ML Internship, I built a pipeline to rank which of 30,000 pages a content team should review first, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, compared to 0.24 for the baseline rule — a result scoped to this training exercise, not a production benchmark.

**Analysis:**
- **What changed in the prompt:** Added explicit constraints on tone, banned buzzwords, and blocked production/success claims beyond what was measured.
- **What improved in output:** Now honest, specific, and correctly scoped — it distinguishes a training-exercise result from a production benchmark without needing a human edit afterward.
- **What still failed:** This is still a summary prompt — it can only restate what it's told. If the input facts were wrong, the model would repeat the error with the same confidence. No prompt-level constraint fixes a bad input; that still needs a human fact-check step.
- **What to try next:** Add a verification layer instructing the model to flag anything it's asserting that wasn't explicitly provided, rather than smoothing gaps into confident prose.

---

# Version 6 — Verification Requirements

**Layer added:** Verification requirements

**Prompt:**
> Write a summary for an AI/ML hiring manager explaining what I built. Context: I worked on the FlyRank ML Internship Content Refresh Prioritization project. I ran the starter pipeline on a 30,000-page dataset. I tested Logistic Regression, Decision Tree, and Random Forest models. Random Forest achieved 0.74 Precision@50 compared to 0.24 baseline in this evaluation setup. Write exactly two sentences: one for problem and approach, one for the measured result. Voice: direct, technical, honest, clear. Avoid buzzwords. Do not claim production readiness. Verification requirements: only use facts explicitly provided in the context; do not add assumptions about business impact, deployment, or success; if any claim cannot be supported by the context, mark it as unsupported instead of writing it.

**Generated output:**
> I worked on the FlyRank ML Internship's Content Refresh Prioritization project, running the starter pipeline on a 30,000-page dataset and testing Logistic Regression, Decision Tree, and Random Forest models to rank pages for review. Random Forest achieved 0.74 Precision@50 compared to a 0.24 baseline in this evaluation setup.

**Stress test — fully missing context:**

**Prompt:**
> Write a technical summary of my ML project for an AI/ML hiring manager. Context: [Insert verified project facts here]. Requirements: explain the problem, approach, and measured result; use only facts explicitly provided; do not invent metrics, deployment status, or business impact; avoid buzzwords; use direct technical language; if information is missing, state that it is unknown instead of assuming; keep the explanation concise and suitable for a portfolio.

**Generated output:**
> Unknown. No project context was provided in this prompt — the context field contains only the placeholder text "[Insert verified project facts here]." I cannot explain the problem, approach, or measured result without that information. Please provide the verified project facts (dataset, models tested, metric, results) and I will write the summary from them.

**Analysis:**
- The model correctly identified missing context rather than filling the gap from memory or invention.
- It avoided using unsupported information, refusing to generate a summary from an empty context field.
- This proves verification works for **fully missing context** — a clean, unambiguous gap.
- It does not prove the same discipline holds under **partial missing context** (e.g., dataset and models given, but the Precision@50 numbers withheld) — a harder case, since a mostly-complete paragraph is more tempting to finish with a plausible-sounding invented number than an empty one is. This is a needed future test, not yet performed.

---

# Final Reusable Prompt

> **Role:** You are writing a technical project summary for an AI/ML hiring manager or recruiter evaluating a candidate.
>
> **Context:** [Insert verified project facts here — problem being solved, dataset, method/pipeline used, models or approaches tested, evaluation metric, and measured results. Do not include unverified numbers or claims.]
>
> **Output requirements:**
> - Write exactly two sentences: one explaining the problem and approach, one stating the measured result.
> - Voice: direct, technical, honest, clear. No buzzwords (avoid words like "innovative," "cutting-edge," "revolutionize," "leverage").
> - Do not claim production readiness, deployment, or business impact unless explicitly stated in the context.
>
> **Verification rules:**
> - Use only facts explicitly provided in the context above.
> - Do not invent metrics, results, or outcomes.
> - Do not assume success, generalization, or real-world impact beyond what is stated.
> - If a claim cannot be supported by the provided context, state that it is unknown or unsupported instead of writing it.

---

# Final Reflection

Each layer fixed a different failure mode, not the same one repeated:

- **Goal** reduced ambiguity — the model had a task instead of an open invitation to write anything.
- **Audience** improved communication style — the tone shifted toward what a hiring manager expects, though this alone didn't add truth.
- **Context** improved factual accuracy — this was the first version that was actually about the real project instead of a generic placeholder.
- **Format** improved structure — constraining to two sentences forced density and cut drift.
- **Constraints** reduced overclaiming — banning specific buzzwords and unearned claims closed the gap between "accurate" and "honest."
- **Verification** improved reliability — instead of trusting that the output happened to be accurate, the prompt made accuracy an explicit, testable requirement, with a defined failure behavior (state "unknown") instead of a silent one (invent something plausible).

The biggest improvement across the ladder came from controlling two separate things, not one: **the information provided to the model**, and **the claims the model is allowed to make with that information**. Context without constraints (Version 3) produced accurate facts wrapped in overconfident language. Constraints without context (Version 2) produced honest-sounding but empty text. Only once both were present together did the output become something that could actually go on a portfolio without a human rewrite.
