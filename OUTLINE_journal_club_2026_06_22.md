# Journal Club — Use of AI in Preclinical Development & Target Selection

**Date:** 22 June 2026
**Speaker:** Florian Wessel, Head of Data Science, SOTIO
**Audience:** All SOTIO employees (voluntary, mixed scientific & non-scientific)
**Length:** 40–45 min talk + 15–20 min Q&A
**Tone:** High-level, accessible to non-preclinical experts
**Structure:** Part 1 = SOTIO/Kraken (intro + concrete story) → Part 2 = External / general AI in preclinical

**Slide budget:** ~31 slides (≈1.4 min per slide on average — some go faster as section dividers, some land for 2–3 min).

**Status:** Outline approved by Flo on 21 May 2026 with the following tweaks (now incorporated below):
- Slide 3 (team intro) — leave as placeholder; Flo will fill in later.
- Old slides 5 + 6 merged → new slide 5 (Task + requirements, with therapeutic window and competition as the illustrative examples).
- Old slides 7 + 8 merged → new slide 6 (Kraken intro with the Kraken image in the background, showing the requirement → data-source mapping; absorbs the data-wheel visual).

---

## OPENING (3 slides · ~3 min)

### 1. Title slide *(already in scaffold)*
- Use of AI in preclinical development and target selection process
- Journal Club · 22 June 2026
- Florian Wessel, Head of Data Science

### 2. Agenda
- Part 1 — How we do it at SOTIO
  - The New Targets team and our problem
  - Kraken: our target discovery platform
  - Where AI enters
  - Results and outlook
- Part 2 — How the field does it (and where it's going)
  - Why AI now
  - AI across the preclinical pipeline
  - From hype to clinic — and the limits

### 3. About the team & me
- New Targets / Data Science team — who we are, what we do (1–2 sentences)
- Photo or team chart if you have one (otherwise plain text + role bullets)
- My background in one line ("…from X to data science for ADC target discovery at SOTIO")
- Lead into the question that defines our work

---

## PART 1 — HOW WE DO IT AT SOTIO (≈18 slides · ~22 min)

### 4. Section divider — "Part 1: How we do it at SOTIO"

### 5. Why this question matters — the bispecific ADC opportunity
- One sentence on what an ADC is (for non-scientists): "antibody = the GPS, payload = the bomb"
- What a *bispecific* ADC adds: two targets at once → better tumor selectivity OR broader coverage
- Why SOTIO cares (1 line)
- *(no past-deck slide for this one — we draft from scratch, simple cartoon if possible)*

### 6. The task: find the right pair out of millions
- ~3,500 surface-protein candidates → **~6 million possible pairs**
- Each pair must satisfy multiple criteria: tumor coverage, healthy-tissue safety, druggability, competition, etc.
- "We can't run 6 million wet-lab experiments. So we built a tool."
- *(text + simple math; could re-use Kraken in Numbers stats from past deck)*

### 7. Kraken — what it is, in one slide
- One-line definition: "Bispecific ADC target discovery platform — integrates ~10 data sources, scores every gene pair on 25+ metrics, supports our entire target-selection workflow."
- Kraken logo (assets/kraken.png) prominent
- URL: kraken.sotio.com
- One-line summary of two deliverables: **Interactive Dashboard** + **Automated Analysis**
- *(adapt slide 5 from 260414 deck — but trim text)*

### 8. The data we integrate
- The "data wheel" graphic from past decks (slide 4 of 260414, the one with Expression / Genomic Alterations / Synthetic Lethality / Competitive Intel / Protein Expression / Protein & Biological Context / Internalization / Knowledge Base / scRNA-seq spokes)
- Subtitle: "10 data sources, ~40 GB locally + live APIs"
- *(re-use the existing visual exactly; text-wise, possibly shorten labels)*

### 9. The heart: mRNA expression in tumors vs healthy tissue
- TCGA (10,000+ tumor samples) vs GTEx (8,000+ healthy samples) — both processed by Toil pipeline (eliminates batch effects)
- Why this matters: "Therapeutic window" — express in tumor, NOT in healthy tissue
- *(re-use slide 8 from 260414 deck — the GTEx/TCGA Toil image)*

### 10. AND-gate vs OR-gate — the bispecific design choice
- Cartoon: two cells, two targets
- AND-gate: both targets on the *same* tumor cell → maximum selectivity
- OR-gate: either target sufficient → broader patient coverage / heterogeneity
- One sentence on trade-off
- *(re-use slide 16 from 251204 deck — the AND vs OR gate visual)*

### 11. Tumor coverage — what the output looks like
- A real screenshot of AND-gate or OR-gate tumor coverage from a recent deck (slide 9 or 10 of 260414)
- Annotation: "Each cell = one cancer type. Color = % of patients where both targets are co-expressed above the safety threshold."
- "This is the kind of insight that used to take weeks of analysis per pair."

### 12. The other 23 metrics, briefly
- Two-column layout listing metric categories with one-line descriptions:
  - Differential expression (AND/OR coverage)
  - Surface localization (GESP, UniProt transmembrane)
  - **Protein copy numbers** (Pan-Cancer Proteome Atlas, CPTAC)
  - Internalization & trafficking (curated + endocytic motif scan)
  - Synthetic lethality (DepMap CRISPR + SynLethDB)
  - Competition (4,954 ADC programs from GlobalData/Beacon)
  - Indication prioritization (epidemiology)
- *(simplified version of slide 14 from 20251023 deck — keep visual, redo text)*

### 13. Interactive dashboard — kraken.sotio.com
- Screenshot of Kraken landing page or Expression page
- Bullet: "Used by the New Targets team — and increasingly the whole company"
- "Anyone at SOTIO with access can explore the data for any gene pair"
- *(re-use slide 6 from 260414 deck — Kraken screenshot)*

### 14. Beyond one-pair-at-a-time: automated analysis
- Three-step diagram: **Define Target Pool → Calculate Metrics → Exhaustive Pairwise Analysis**
- "600,000+ scored data points per run — what would take a person months runs overnight."
- *(re-use slide 7 from 260414 deck)*

### 15. Two strategies for the target pool
- **PIONEER:** Top 25% GESP score genes minus already-developed targets. Undeveloped surface proteins; freedom to operate; higher risk.
- **SPOTLIGHT:** Competitor targets whose highest stage is preclinical, not yet combined. Novel pairings of partially-validated targets; lower risk, more competitive.
- *(re-use slide 21 from 260414 deck — PIONEER / SPOTLIGHT)*

### 16. The target funnel — concrete numbers
- 186 unique genes → 82,498 combinations tested → AI advanced 77 → Scientists agreed on 58 → 12 recommended → translational & BCT review → **6 T1 + 10 T2 recommended targets**
- Visual funnel with real numbers
- *(re-use slide 24 from 260414 — Target Evaluation Progress with the 186/77/58/12/6 funnel)*

### 17. Recommended targets — the punch line
- **T1 Recommended (6):** TNFRSF12A, TSPAN8, CLDN3, MMP14, EPHB2, EMP2
- **T2 Conditional (10):** ITGB4, PODXL, FZD2, ST14, BST2, DCBLD2, PLXNB2, IL1RAP, EFNB2, PLXND1
- "From 6 million theoretical pairs to a focused shortlist of ~16 candidates in roughly 6 months."
- *(can re-use the bottom of slide 24, blown up)*

### 18. "Adding a brain to the Kraken" — where AI enters
- Diagram of the AI-assisted workflow (slide 17 from 260414): Claude + Gemini Deep Research assess ADC suitability → local AI model combines and structures → Knowledge Base populated → scientists validate & resolve disputes
- Frame as: "Same data we always had — but the literature triage that used to take weeks now happens in hours."
- *(re-use slide 17 from 260414)*

### 19. AI vs scientists — did it actually work?
- Confusion matrix / agreement chart from past decks (slide 18 of 260414, or slides 6–8 of 20260305)
- Headline: **Claude outperformed Gemini.** Scientists are most conservative, agreed most often with Claude.
- Cost callout: "~$150–330/month for Claude + Gemini access" — vs scientist time saved
- *(this is the CSO-sanctioned slide — lean into it. Re-use the existing visuals.)*

### 20. Kraken Evolution — Descriptive Today → Predictive Tomorrow
- The three-arrow roadmap diagram (slide 50 from 260414 or slide 22 from 251204)
- Descriptive (today) → Predictive (ML on ~5,000 clinical ADC programs) → Active learning (feedback loop)
- "We're at the first arrow. The next two are where this gets really interesting."
- *(re-use the existing diagram exactly)*

### 21. SOTIO part — summary slide
- 3 bullets:
  - **Scale:** ~6M possible pairs → 25+ metrics each → automated, reproducible
  - **AI today:** Literature triage + Knowledge Base population — validated against scientists
  - **AI tomorrow:** Predictive scoring + active learning loop
- "AI doesn't replace the scientists. It lets us ask 100× more questions in the same time."

---

## TRANSITION (1 slide · ~30 sec)

### 22. Section divider — "Part 2: How the field does it"
- One-liner: "What we built fits into a much bigger picture — let's zoom out."

---

## PART 2 — EXTERNAL VIEW (≈10 slides · ~13 min)

### 23. Why drug discovery is hard
- 3 large stats: **~$2.6B** average per approved drug · **10–15 years** discovery → approval · **~90%** of clinical candidates fail
- "Most fail in Phase II — for efficacy or safety. AI's promise: catch these earlier, cheaper."
- *(adapt slide 2 of AI_in_Preclinical_Development.pptx)*

### 24. The preclinical pipeline — and where AI plays
- 5-stage horizontal flow: Target ID → Target Validation → Hit Discovery → Lead Optimization → Candidate Selection
- Under each, one "AI EXAMPLE" tag (omics mining, safety prediction, virtual screening, generative design, clinical-risk prediction)
- *(re-use slide 3 of AI_in_Preclinical_Development.pptx — already well-designed)*

### 25. Why AI in drug discovery, why now
- 3 columns: **Biological data at scale · Compute & specialized hardware · Mature ML models**
- Subtitle: "Three things came together in the last decade — tasks that took a year of bench work can be triaged in days."
- *(re-use slide 4 of AI_in_Preclinical_Development.pptx)*

### 26. AI for target identification
- 4 quadrants: Multi-omics integration · Knowledge graphs · Image-based phenotyping · Patient data mining
- "Out of ~20,000 human genes, which one should we drug?"
- Optional callout: "This is what Kraken does for surface proteins."
- *(re-use slide 5 of AI_in_Preclinical_Development.pptx)*

### 27. AI for target validation & prioritization
- 4 quadrants: Disease relevance · Safety window · Druggability · Competitive landscape
- "Hundreds of questions in the time it used to take to ask one."
- *(re-use slide 6 of AI_in_Preclinical_Development.pptx)*

### 28. AI for designing the molecule
- Two halves: **AlphaFold / ESMFold etc.** (predict any 3D structure in minutes — 200M+ structures freely available) and **Generative design / RFdiffusion** (design molecules that fit a pocket)
- "Structure is what drugs grab onto. Until 2021, getting one took years."
- *(re-use slide 7 of AI_in_Preclinical_Development.pptx)*

### 29. From hype to clinic — it's already happening
- 4 example companies: Insilico (fibrosis drug, AI-identified target → Phase II in record time) · Isomorphic Labs (DeepMind spin-off; multi-billion Novartis & Lilly deals) · Recursion / Exscientia (image- and ML-driven; multiple molecules in trials) · BenevolentAI (knowledge graphs; baricitinib for COVID in days)
- *(re-use slide 8 of AI_in_Preclinical_Development.pptx)*

### 30. The honest view — what AI still can't do
- 6 short bullets with icons: Data bottleneck · Correlation ≠ causation · Validation gap · Hallucinated chemistry · Bias toward known biology · Regulatory acceptance
- "AI is a powerful collaborator, not an autonomous discovery engine."
- *(re-use slide 9 of AI_in_Preclinical_Development.pptx)*

### 31. Where this is heading
- 3 bullets with icons: **Foundation models for biology** · **Closed-loop labs** (AI proposes → robots test → results retrain) · **Patient-specific targets** (true precision oncology)
- *(re-use slide 10 of AI_in_Preclinical_Development.pptx)*

---

## CLOSING (2 slides · ~2 min)

### 32. Take-aways
- AI in preclinical is a **collaboration tool**, not a replacement. The best results come from combining domain experts with the right model on the right data.
- At SOTIO, Kraken already operationalizes this for bispecific ADC target discovery — and the AI-assisted literature review delivered a validated shortlist faster than would have been possible otherwise.
- The next steps for us: predictive ML on ADC outcomes, and tighter feedback loops between in-silico predictions and wet-lab results.

### 33. Thank you / Questions
- *(use end slide from scaffold)*

---

## What I need from you before I start building

1. **Approve / edit the outline.** Slide-by-slide is fine — say "drop slide N", "merge N and M", "swap order of N and O", etc.
2. **Team intro (slide 3).** One sentence about who's on the New Targets team and what each role does — or, if simpler, the names + roles. I'll format it.
3. **Slide 5 ("Why bispecific ADCs matter").** Do you have a SOTIO-specific framing (e.g. an existing pipeline diagram) you want me to reference, or should I draft a simple ADC + bispecific ADC cartoon from scratch?
4. **Kraken screenshots for slide 13.** Should I get the screenshot from the past decks (slide 6 of 260414 — current is fine), or do you want to grab fresh screenshots of the latest UI (Expression / Knowledge Base / Analysis Explorer pages) to drop in?
5. **Anything missing.** Is there a topic, slide, or message you want included that I haven't accounted for? (E.g. specific scRNA-seq slide, ADC discovery timeline, anything indication-related.)
