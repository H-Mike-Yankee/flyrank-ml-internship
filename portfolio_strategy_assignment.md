# AI Portfolio Strategy — Submission
**Mahmood Yaqub**
FlyRank AI & ML Internship — Portfolio Assignment

---

## Part 1 — Portfolio Strategy (One Person, One Claim, One Action)

| Element | Definition |
|---|---|
| **One Person** | AI/ML recruiters and engineering hiring managers screening candidates for internship and entry-level AI/ML roles |
| **One Claim** | *"I build AI-powered backend applications using Python, FastAPI, Machine Learning, and NLP to solve real-world problems in healthcare and recruitment. I am continuously expanding my expertise in production practices, cloud technologies, and MLOps."* |
| **One Action** | Contact me for AI/ML internship or full-time opportunities |

**Why this works:** The claim separates demonstrated skill (first sentence — backed by HealthAI, the AI Resume Screening System, and internship project contributions) from skill in active development (second sentence — production practices, cloud, MLOps). This replaced an earlier "production-ready" claim that could not be fully defended under interview questioning, particularly around deployment ownership.

---

## Part 2 — Recruiter-Focused Sitemap

```
Home
├── Projects
│   └── /projects/[project-slug]   (individual case study per project)
├── About        (includes current student status: BS Computer Science, 2022–2026)
├── Resume       (downloadable PDF)
└── Contact
```

| Page | Why it exists | What belongs there | How it supports the goal |
|---|---|---|---|
| **Home** | First impression; states the claim immediately | Proof statement above the fold, top 2–3 projects, persistent CTA | Filters recruiters toward deeper reading within seconds |
| **Projects** | The evidence layer | Grid of real projects, each linking to a full case study | Proves the claim with specifics — no evidence, no credibility |
| **About** | Explains engineering process, not life story | Working style, tools, current student status, current FlyRank focus | Supports "problem-solving" claim with how-I-think content |
| **Resume** | Expected by every recruiter | Downloadable PDF, always accessible | Reduces bounce risk; primary screening document |
| **Contact** | Conversion point | Email, LinkedIn, GitHub | This is the entire goal of the site |

---

## Part 3 — Claude Project Custom Instructions

```
You are my AI mentor and portfolio tutor.

Proof statement:
"I build AI-powered backend applications using Python, FastAPI, Machine 
Learning, and NLP to solve real-world problems in healthcare, recruitment, 
and automation. I am continuously expanding my expertise in production 
practices, cloud technologies, and MLOps."

Target audience: AI/ML recruiters and engineering hiring managers.
Primary action: Get contacted for AI/ML internship or full-time roles.

Rules:
- Act as a tutor, not an answer machine. Ask clarifying questions before 
  producing content when information is missing or ambiguous.
- Challenge weak or unsupported claims directly and explain your reasoning.
- Never invent projects, metrics, achievements, or experience I haven't 
  described to you. If unsure whether something is true, ask.
- Prioritize technical accuracy over polish. A confident but inaccurate 
  claim is worse than an honest, modest one.
- Keep recruiter attention span in mind: content should work at both a 
  6-second skim and a 5-minute deep read.
```

---

## Part 4 — Pressure-Test Prompt

```
Act as a skeptical senior AI engineer and technical recruiter reviewing my 
portfolio strategy before I ship it. Critically evaluate my claim, sitemap, 
and overall recruiter journey. Do not default to agreement or encouragement.

Specifically:
1. Is my claim supported by evidence I've actually described, or is it 
   overclaiming? Where exactly would this fall apart in an interview 
   follow-up question?
2. Does my sitemap guide a recruiter toward my primary action within 
   3 clicks, or does it require too much digging?
3. What's the single weakest link in the journey from "recruiter lands on 
   Home" to "recruiter contacts me" — and why?
4. What would you cut, and what's missing entirely?

Give me blunt, realistic feedback — not motivational filler.
```

---

## Part 5 — Pressure-Test Results

**Three strengths**
1. **HealthAI is unambiguous, solo-owned, full-stack evidence** — backend, frontend, auth, admin-controlled model retraining, and a self-prepared dataset. This is a genuinely above-average junior portfolio piece.
2. **The work history tells a coherent, progressing story**: Backend Developer → AI Intern → current Machine Learning Intern at FlyRank, alongside a part-time analyst role. The trajectory itself is a signal of intentional direction toward AI/ML.
3. **Every claim on the final resume can survive a follow-up question**, because inaccurate or overstated claims (full solo ownership of a Docker/AWS deployment, an unqualified "production-ready" label, unclear scraper project identity) were identified and corrected before submission.

**Three weaknesses**
1. **FlyRank, the most current and most relevant role, is still learning-stage** — no shipped deliverable yet. The Projects page has to carry the technical proof; the current-role section cannot yet do that work.
2. **Only 2 of 4 technical projects (HealthAI, AI Resume Screening System) are under full individual ownership.** The other two (Nutrition API, Play Store Scraper) involved team/internship collaboration, so depth of ownership varies across the portfolio and must be represented accurately per project.
3. **Bajwa Trader, while honestly disclosed, is off-narrative** for an AI/ML-focused portfolio — necessary for accuracy, not persuasive for the core claim.

**Three improvements**
1. Be ready to explain, unprompted, why Sentence Transformers (semantic similarity) was chosen over keyword matching in the Resume Screening System — the most technically distinctive design decision in the portfolio.
2. Update the FlyRank entry with a concrete outcome (a specific model result or EDA finding) once available — it is currently process-described rather than outcome-described.
3. Add a short "currently learning" note (About page) naming deployment/MLOps as an active growth area — naming a real gap is more credible than implying it's already closed.

---

## Part 6 — Reflection

During this assignment, I realized that some of my original portfolio and resume statements were broader than my actual contributions. For example, I initially described a Docker and AWS deployment as if I had completed it independently, when in reality it was a collaborative team effort during my internship. The pressure-testing process helped me identify unclear project ownership, deployment claims, and overlapping work experiences.

I revised my proof statement, clarified the distinction between personal projects and internship work, and accurately described my individual contributions instead of overstating them. These changes made my portfolio more credible, technically accurate, and easier to defend during interviews.

One area that is still evolving is my current FlyRank internship, where I am continuing to build practical machine learning experience. As I complete more assignments and real deliverables, I plan to update my portfolio with measurable outcomes and stronger evidence of my skills.

---

## Part 7 — Submission Notes

This submission reflects an iterative pressure-testing process. The initial proof statement and resume contained claims — full solo ownership of a Docker/AWS deployment, an unqualified "production-ready" label, and an unclear work history — that did not fully match verified reality. Through structured critical review, each claim was checked against actual project scope and individual contribution, and revised accordingly. This included reframing team contributions honestly, separating internship experience from personal projects, correcting a mismatched project description (LinkedIn vs. Play Store scraper), and adjusting the core proof statement to match demonstrable skill level rather than aspirational language.

The final portfolio strategy, sitemap, and resume prioritize technical accuracy and interview defensibility over surface-level polish.

---

## Appendix — Finalized Resume Experience Section

**Professional / Internship Experience**

```
FlyRank — Machine Learning Intern
July 2026 – Present
  - Executing and analyzing machine learning pipelines using Python and 
    Jupyter Notebooks on anonymized search datasets.
  - Performing exploratory data analysis, feature engineering, and model 
    evaluation while completing real-world ML assignments under mentorship.
  - Learning practical machine learning workflows, decision trees, baseline 
    models, and model interpretation through the FlyRank AI & ML Internship.

A2Z Tech (Official) — AI Intern
June 2024 – August 2024
  - Contributed to an AI-powered Nutrition & Workout Recommendation API: 
    built FastAPI backend logic and a Random Forest model for personalized 
    meal/workout plans; collaborated on containerizing and deploying the 
    application with Docker on AWS (ECR) as part of a team.

Digital Upgraders LLC — Backend Developer
May 2023 – July 2023
  - Built a Google Play Store App Scraper: FastAPI backend, Selenium/
    BeautifulSoup scraping, MongoDB storage with deduplication, CSV export 
    with filtering; deployed on a server for scalable access.

Bajwa Trader — Data Analyst (Part-time, 1 day/week)
February 2024 – Present
  - Managed stock records and profit & loss analysis to support business 
    decisions.
```

**Personal Projects**

```
HealthAI — Disease Prediction & Healthcare Management System
  Solo-built full-stack application (Next.js, FastAPI, Random Forest) trained 
  on a public medical dataset prepared for training and evaluation. Built 
  independently: backend, frontend, JWT authentication, prediction workflow, 
  analytics dashboard, and admin-controlled model retraining.

AI-Powered Resume Screening System
  FastAPI + MongoDB + Sentence Transformers. Semantic resume-to-job-description 
  matching, JWT authentication, multi-format uploads (PDF/DOCX/TXT/ZIP), 
  candidate ranking and screening history.
```
