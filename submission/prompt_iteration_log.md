# Prompt Iteration Log

## 1. Task

Generate a technical summary of my FlyRank ML Internship Content Refresh Prioritization project, for an AI/ML hiring manager reading a portfolio.

---

## 2. Version 0 — Naive Prompt

**Prompt:**
> Write about my project.

**Generated output:**
> I recently worked on an exciting project that showcases the power of data-driven innovation. Using cutting-edge technology, I developed a solution that transforms raw information into actionable insights, driving impactful results and unlocking new possibilities. This project demonstrates strong technical skills and a passion for solving real-world problems through smart, scalable solutions.

**What changed:** Nothing yet — this is the unmodified starting point.

**What improved:** N/A.

**What still failed:** No real content. No dataset, no model, no metric — could describe any project. Buzzword-heavy ("cutting-edge," "unlocking new possibilities") with nothing behind it.

**Next improvement:** Give the model a role, so it writes from a defined perspective instead of a generic one.

---

## 3. Version 1 — Role Assignment

**Technique added:** Role Assignment (exactly one technique — no other changes)

**Prompt:**
> You are an AI/ML engineer writing a professional project summary for a hiring manager. Write about my project.

**Generated output:**
> As an AI/ML engineer, I built a machine learning system to solve a practical business problem. The project involved analyzing data, training models, and delivering a solution that improves decision-making. This work reflects a solid understanding of the machine learning lifecycle, from data preparation through model evaluation, and demonstrates the kind of applied technical skill hiring managers look for.

**Prompt change:** Added a role instruction — the model now writes as an AI/ML engineer addressing a hiring manager, rather than an unspecified narrator.

**Output difference:** Tone became more professional and structured — it now references a "lifecycle" (data prep, training, evaluation) rather than vague inspiration language.

**Remaining problem:** Still zero real facts. No project name, no dataset, no model, no number. The role changed the voice, not the substance — it's still describing a hypothetical project, not this one.

**Next improvement:** The model needs actual project facts and a reason the project exists, or it will keep inventing generic-but-plausible detail to fill the role convincingly.

---

## 4. Version 2 — Context and Motivation

**Technique added:** Context and Motivation

**Prompt:**
> You are an AI/ML engineer writing a professional project summary for a hiring manager. Context: FlyRank content teams manage thousands of pages per client and cannot manually review each one to decide what needs attention. Existing rule-based flags catch some patterns but miss interactions between signals. As part of the FlyRank ML Internship, I worked on Lane 2 (Content Refresh Prioritization) — ranking which of 30,000 pages should be reviewed first. I ran the starter pipeline (01_prepare_features → 02_baseline_score → 03_train_model → 04_evaluate_and_export → 05_build_pdf_report), testing Logistic Regression, Decision Tree, and Random Forest models, evaluated with Precision@50. Random Forest reached 0.74 Precision@50 versus 0.24 for the baseline, using a client-holdout split (27,675 training rows, 2,325 test rows). Write about my project.

**Generated output:**
> FlyRank's content teams manage thousands of pages per client and can't manually review each one to identify what needs attention — existing rule-based flags catch some patterns but miss the interactions between signals. As part of the FlyRank ML Internship, I worked on Lane 2 (Content Refresh Prioritization), using the starter pipeline to rank which of 30,000 pages should be reviewed first. I ran the starter pipeline — from feature preparation through model training and evaluation — testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the metric, using a client-holdout split of 27,675 training rows and 2,325 test rows. Random Forest reached 0.74 Precision@50, a substantial improvement over the 0.24 baseline, showing that a learned ranking can capture patterns a fixed rule misses.

**Prompt change:** Added the actual motivation (why the problem exists) and the real, verified project facts — dataset size, pipeline stages, models, metric, split, and results.

**Output difference:** Now this is genuinely about the real project — correct numbers, correct pipeline stages, correct split. This is the first version with real content instead of a plausible-sounding placeholder.

**Remaining problem:** "A substantial improvement" and "showing that a learned ranking can capture patterns a fixed rule misses" both drift into a more confident, conclusive tone than the actual scope supports — this was one evaluation on a starter dataset, not a general proof. There's also no length or structure constraint, so the output ran long and unstructured.

**Next improvement:** Show the model concrete examples of the tone and scope it should match, so it stops drifting into overconfident summary language on its own.

---

## 5. Version 3 — Few-shot Examples

**Technique added:** Few-shot Examples

**Prompt:**
> You are an AI/ML engineer writing a professional project summary for a hiring manager. Context: [same context and verified facts as Version 2]. Match this style:
>
> Example (good): "I built a classifier to flag at-risk accounts using historical transaction data. The model reached 82% recall on held-out data, compared to 60% for the existing rule — a result scoped to this evaluation, not a production benchmark."
>
> Example (bad): "I leveraged cutting-edge AI to revolutionize account risk detection, delivering game-changing results for the business."
>
> Write about my project in the style of the good example, not the bad one.

**Generated output:**
> I built a pipeline to rank which of 30,000 pages should be reviewed first, as part of the FlyRank ML Internship's Content Refresh Prioritization project (Lane 2). Testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the metric on a client-holdout split, Random Forest reached 0.74 Precision@50 compared to 0.24 for the baseline — a result scoped to this evaluation setup, not a production benchmark.

**Prompt change:** Added one paired example (good vs. bad) demonstrating the target tone and the explicit scope-qualifier pattern ("a result scoped to this evaluation, not a production benchmark").

**Output difference:** The overconfident language from Version 2 is gone. The model picked up the specific scoping phrase pattern from the good example almost directly, and dropped the unscoped claim ("substantial improvement," "capture patterns a fixed rule misses") entirely.

**Remaining problem:** The output length and paragraph structure still aren't fixed — this run happened to be reasonably tight, but nothing in the prompt guarantees consistent length or a specific structure (e.g., problem vs. result split) across repeated runs.

**Next improvement:** Add an explicit output structure so the format doesn't depend on the model happening to imitate the example's length.

---

## 6. Version 4 — Output Structure

**Technique added:** Output Structure

**Prompt:**
> [Same role, context, and few-shot example as Version 3.] Write exactly two sentences: the first stating the problem and approach, the second stating the measured result. Do not add anything beyond these two sentences.

**Generated output:**
> I built a pipeline to prioritize which of 30,000 pages a content team should review first, testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, compared to 0.24 for the baseline rule.

**Prompt change:** Added an explicit structural requirement — exactly two sentences, each with a defined job.

**Output difference:** Now consistently tight and predictable in shape — no matter what the model might otherwise add, the structure forces problem+approach into one sentence and result into the other. This is now close to a drop-in portfolio line.

**Remaining problem:** The structure only controls *shape*, not *reasoning*. The model is asked to produce a final two-sentence answer directly — nothing requires it to first work out which facts matter most or check them against each other before writing. If the context were longer or messier, this version offers no safeguard against skipping a key fact or misordering an idea.

**Next improvement:** Force the model to work through the reasoning in explicit steps before producing the final two-sentence output.

---

## 7. Version 5 — Step Decomposition

**Technique added:** Step Decomposition

**Prompt:**
> [Same role, context, few-shot example, and two-sentence output requirement as Version 4.] Before writing the final summary, work through these steps internally: (1) identify the core problem being solved, (2) identify the approach and method used, (3) identify the single most important measured result, (4) check that no claim goes beyond what was explicitly provided. Then output only the final two-sentence summary — do not show your steps.

**Generated output:**
> I built a pipeline to prioritize which of 30,000 pages a content team should review first, as part of the FlyRank ML Internship's Content Refresh Prioritization project — testing Logistic Regression, Decision Tree, and Random Forest models with Precision@50 as the evaluation metric. Random Forest reached 0.74 Precision@50 in this evaluation setup, compared to 0.24 for the baseline rule.

**Prompt change:** Added explicit internal reasoning steps (identify problem → identify approach → identify result → check for unsupported claims) before the model produces its final answer.

**Output difference:** Nearly identical to Version 4's output — the biggest visible change is that "FlyRank ML Internship's Content Refresh Prioritization project" is now explicitly named in sentence one, which Version 4 had left implicit. The self-check step (4) appears to have reinforced, not changed, the scoping language already established in Version 3.

**Remaining problem:** On a short, already-clean prompt like this one, the visible benefit of step decomposition is small — the task was simple enough that the model didn't need explicit reasoning steps to get it right. This technique likely matters more on harder, multi-fact or ambiguous tasks than on a two-sentence summary from a short, clean context.

**Next improvement:** Test step decomposition on a harder task — for example, asking the model to also decide *which* of several possible facts to include when the context has more information than fits in two sentences — where reasoning steps would have more to actually do.

---

## 8. Cross-Model Comparison (Claude vs. ChatGPT)

To complete the assignment, I ran the final Version 5 prompt on both Claude and ChatGPT using the same context and instructions.

| Aspect | Claude | ChatGPT |
|---|---|---|
| Tone | Direct, restrained, and highly literal | Slightly smoother and more conversational while remaining professional |
| Accuracy | Stayed within the provided facts and respected the evaluation scope | Also stayed within the provided facts without introducing unsupported claims |
| Structure | Followed the required two-sentence format exactly | Also followed the required two-sentence structure exactly |
| Strength | Very careful about qualifying the result as an evaluation outcome rather than a production claim | Produced a slightly more natural flow while preserving the required technical details |
| Weakness | More concise, leaving less explanatory context | Slightly more likely to add connecting phrases if constraints are relaxed |

**Observations**

Both models produced technically correct summaries because the final prompt supplied clear context, explicit structure, and strong constraints. The largest improvement came from the prompt itself rather than the model. Once the context, examples, structure, and reasoning steps were provided, the differences between Claude and ChatGPT became relatively small.

Claude tended to be more conservative in its wording, while ChatGPT produced slightly smoother transitions between ideas. Neither model invented metrics, deployment claims, or business impact because the prompt explicitly prohibited unsupported claims.

**Conclusion:** The quality of the final result depended more on prompt engineering than on the choice of model. A well-designed prompt reduced variation between the two systems and produced reliable, reusable output.

---

## 9. Final Reusable Prompt Template

> **Role:** You are an AI/ML engineer writing a professional project summary for a hiring manager evaluating a candidate.
>
> **Context:** [Insert: the problem your project addresses and why it matters — who faces this problem and what's inadequate about the current approach. Insert: your verified project facts — dataset, method/pipeline, models or approaches tested, evaluation metric, and measured results. Do not include unverified numbers or claims.]
>
> **Style example (match this):**
> "I built [a system] to [solve X] using [method]. The result reached [metric] on [evaluation setup], compared to [baseline] — a result scoped to this evaluation, not a production benchmark."
>
> **Avoid this style:**
> "I leveraged cutting-edge AI to revolutionize [X], delivering game-changing results."
>
> **Output structure:** Write exactly two sentences — sentence one states the problem and approach, sentence two states the measured result. Add nothing beyond these two sentences.
>
> **Before writing, work through these steps internally (do not show them):**
> 1. Identify the core problem being solved.
> 2. Identify the approach or method used.
> 3. Identify the single most important measured result.
> 4. Check that no claim goes beyond what was explicitly provided in the context.
>
> **Rules:** Use only facts explicitly provided in the context. Do not invent metrics, results, deployment status, or business impact. If a claim cannot be supported by the context, state that it is unknown instead of writing it.

---

## 10. Reflection

**Technique that improved the output most:** Context and Motivation (Version 2). This was the point where the output stopped being generic and started being about the real project — every later technique refined tone, shape, or reasoning, but none of them added *substance*. Without real facts, no amount of structure or examples produces a truthful summary.

**Technique that helped the least:** Step Decomposition (Version 5), on this particular task. The prompt was short and the facts were already clean and unambiguous by Version 4, so there was little for explicit reasoning steps to actually resolve — the output barely changed. This is an honest "did not improve much" result, not a failure to apply the technique correctly; it likely would matter more on a harder task with more facts to weigh or a messier context.

**What I would improve next:** Test whether Step Decomposition actually earns its place on a harder version of this task — for example, a context with 10+ facts where the model has to choose which 2-3 matter most for a two-sentence summary. That's a case where reasoning steps would have real work to do, unlike the clean, short context used here.

---

## Final Checklist

- [x] Task briefly described (Section 1)
- [x] Version 0 (naive prompt) included with output and four-part analysis
- [x] Version 1 adds exactly one technique (Role Assignment) — no other changes
- [x] Version 2 adds exactly one technique (Context and Motivation) — no other changes
- [x] Version 3 adds exactly one technique (Few-shot Examples) — no other changes
- [x] Version 4 adds exactly one technique (Output Structure) — no other changes
- [x] Version 5 adds exactly one technique (Step Decomposition) — no other changes
- [x] Cross-model comparison (Claude vs. ChatGPT) — completed, Section 8
- [x] Final reusable prompt template included, with all personal/project details replaced by placeholders
- [x] Reflection includes a technique that helped most, a technique that helped least, and an honest "did not improve much" observation
- [x] Only verified facts used throughout — no invented metrics, datasets, results, or business impact
- [x] All claims correctly scoped (training exercise, starter dataset, evaluation setup, no production/causal claims)
