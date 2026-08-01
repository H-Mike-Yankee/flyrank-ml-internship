# Voice Card

Direct, technical, honest, clear, no buzzwords.

Rules applied throughout this document:
- Use verified experience only — no invented results, no rounding up.
- Avoid exaggeration. Scope every claim to what was actually tested.
- Prefer specific examples (real numbers, real file paths, real decisions) over generic claims.
- Keep explanations simple and clear — plain sentences over dressed-up ones.

---

# Content Refresh Prioritization

*FlyRank ML Internship — Lane 2: Refresh / Content Opportunity Scoring*

## Problem

FlyRank works with large volumes of search and content performance data. The hard part isn't the data — it's turning it into decisions. A client can have thousands of pages, and no team can manually review each one to decide what needs attention. FlyRank's existing system uses fixed rules to flag pages, but rules can miss patterns that only show up when several signals interact.

The problem isn't "is this page declining." On the starter dataset, 54.2% of pages showed some decline signal — too broad to act on as a flag. The real problem is prioritization: out of thousands of pages, which ones should a reviewer with limited time check first.

## What I Did

I chose the **Refresh / Content Opportunity Scoring** lane over three other predefined options. The reason: it maps onto a real operational decision, not just a diagnosis. A reviewer with limited weekly time needs a ranked shortlist, not a list of problems. A related lane (CTR/Engagement Scoring) covers one specific signal — pages with visibility but weak clicks — but that's one of several reason codes this broader lane can surface. I treated CTR issues as a subset of the prioritization problem, not a separate one.

**Framed the decision first.** Before building anything, I defined the decision, the actor, and the cost of a wrong call: a reviewer needs the top pages worth checking. A missed declining page (false negative) is more costly than a wrongly flagged one (false positive), because undetected decline compounds silently while wasted review time is a smaller, recoverable cost.

**Checked the data before modeling.** On the starter dataset (30,000 pages, 32 clients): 54.2% of pages flagged as declining, 55.8% with real visibility (500+ impressions in 90 days). Having many pages with decline signals and visibility means a simple threshold would still leave too many pages to review. The problem becomes ranking which pages deserve attention first.

**Ran the pipeline.** I ran the full reference pipeline (`01_prepare_features → 02_baseline_score → 03_train_model → 04_evaluate_and_export → 05_build_pdf_report`) with a client-holdout split — 27,675 training rows, 2,325 test rows, with entire clients held out of training so the model is tested on clients it hasn't seen.

**Respected the leakage boundary.** `trend_direction` and `trend_pct` are the label source in this dataset and are explicitly marked as columns that must never be used as features. I confirmed the model's feature set excludes both.

## What Came Of It

| Method | Precision@50 |
|---|---|
| Baseline (rule-based) | 0.24 |
| Logistic Regression | 0.40 |
| Decision Tree | 0.58 |
| Random Forest | 0.74 |

Precision@50: of the top 50 pages ranked first, how many matched the target label. Random forest outperformed the fixed rule by a wide margin **in this evaluation setup** — a comparison on the starter dataset with a defined split, not a production benchmark.

Top feature signals for the random forest: `days_with_impressions`, `log_impressions_90d`, `avg_position`, `content_age_days`. This matched what I expected — pages with a track record of visibility and reasonable position indicate existing traffic worth maintaining, and age captures the "getting stale" dimension. No single signal dominated, which matches the original framing: no one rule was doing all the work.

## Limitations and Next Steps

- **Leakage checks were verified, not independently rebuilt.** I confirmed via documentation and model configuration that label columns are excluded from features, and that client-holdout prevents the same client appearing in train and test. I have not yet written my own independent checks inside the notebook — an explicit column-exclusion assertion, a client-ID overlap check. That's a concrete next step so the analysis doesn't depend on the pipeline's documentation being correct.
- **No causal claim.** The model shows association between signals and the decline label, not causation. It doesn't say a refresh will cause recovery — that needs an actual experiment.
- **No production claim.** The 0.24 → 0.74 comparison is scoped to the starter dataset and this evaluation setup. It hasn't been tested against FlyRank's live production rules or at full warehouse scale (~79M rows).
- **Next step:** extend to the full warehouse release, add the independent leakage checks above, and move from the current-window proxy label used here to a future-window label (prior 90 days predicting the next 30 days).

---

## About Me

I'm Mahmood Yaqub, an AI Developer focused on Machine Learning, NLP, and backend engineering. I build applications that combine ML models with practical APIs using Python and FastAPI — training models like Random Forest for ranking and classification tasks and integrating models like Sentence Transformers for semantic matching. I'm currently a Machine Learning Intern at FlyRank and a BS Computer Science student (2022–2026). My other work includes HealthAI, a disease-prediction system I built independently end to end, and an AI-powered resume screening system using semantic search.

## Contact

If you're hiring for AI/ML internship or entry-level engineering roles, I'd like to talk.
**Email:** mikeyankee2k0@gmail.com

---

## Before / After: Same Content, Written Two Ways

**Before (generic AI writing style):**
> Leveraging cutting-edge machine learning techniques, this innovative project revolutionizes content prioritization by harnessing the power of AI to unlock actionable insights, driving significant improvements in decision-making efficiency and empowering teams to achieve outstanding results.

**After (voice card applied):**
> A rule-based baseline hit Precision@50 of 0.24. A random forest trained on the same data hit 0.74, in a client-holdout evaluation. This is evidence from one evaluation setup, not a production claim. The next step is testing whether the approach generalizes.

The difference isn't tone — it's information. The "after" version names a real number, states what was and wasn't tested, and gives the reader something to verify. The "before" version could describe any project and proves nothing.
