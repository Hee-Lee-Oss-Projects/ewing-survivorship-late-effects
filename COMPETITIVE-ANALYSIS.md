# Competitive + Improvement Analysis — `ewing-survivorship-late-effects`

> Analyst pass · 2026-06-29 · Sources web-grounded and cited inline. Scope: PLAN.md (v0.1.0,
> 2026-06-28) + TASKS.md. Project = open, education-only survivorship/late-effects resource library
> for Ewing sarcoma survivors across the pediatric → AYA transition, synthesized from vetted bodies
> (NCI/PDQ, COG LTFU, IGHG, ESMO, CCLG). HIGH risk-tier; cancer guardrails apply.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually strong on governance, provenance, and the no-advice boundary — arguably best-in-class
for safety scaffolding. The gaps are mostly in **clinical-domain fidelity**, **currency mechanics**, and a
few **metric/structural** weaknesses. Concrete findings:

**A. Alignment to COG LTFU structure (exposure-based screening) — mostly right, but under-specified.**
- The exposure-keyed content model is correct and matches how COG LTFU v6 actually works: it is an
  *exposure- and risk-based* compendium (165 sections, 45 Health Links in v6.0, released Oct 2023),
  organized so screening is driven by which agents/doses/fields a survivor received
  ([COG LTFU v6 review, PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC12188901/);
  [survivorshipguidelines.org](https://www.survivorshipguidelines.org/)).
- **Gap:** PLAN names exposures generically (`anthracycline`, `radiation:field+dose-band`) but does not commit
  to the **dose-band thresholds** that drive COG/IGHG recommendations (e.g., anthracycline cumulative-dose
  tiers, chest radiation ≥10 Gy as the breast-surveillance trigger per IGHG
  ([JCO OP, IGHG breast](https://ascopubs.org/doi/10.1200/OP-25-01017))). Without explicit, sourced dose-band
  vocabulary in the schema, "exposure-keyed" risks being too coarse to be faithful — or it tips into implying
  personalized risk. This boundary (dose-band education vs. individualized risk) needs an explicit schema rule.
- **Gap:** No mention of COG's own **Health Links** as the structural analog. Health Links are *exactly* the
  plain-language, per-topic patient education layer COG already ships on top of the guidelines
  ([childrensoncologygroup.org/survivorship](https://childrensoncologygroup.org/survivorship/)). PLAN must
  position against them explicitly (see §2) and decide its delta, or it duplicates existing free material.

**B. Treatment-specific late effects — coverage good, two accuracy traps.**
- Cardiac (anthracycline), 2nd malignancy (alkylator/radiation), fertility (alkylator), renal (ifosfamide),
  ototoxicity, neuropathy (vincristine), MSK/growth (surgery+RT), neurocognitive/psychosocial — all the
  high-burden Ewing effects are scoped. Good.
- **Accuracy trap 1 — ototoxicity:** PLAN hedges "where platinum/relevant exposures apply." Standard
  Ewing regimens (VDC/IE — vincristine, doxorubicin, cyclophosphamide / ifosfamide, etoposide) are
  **not platinum-based**; ototoxicity is a weak fit for Ewing unless a specific protocol used platinum.
  Listing it risks a faithfulness/relevance failure. Recommend demoting it to conditional/backlog and
  foregrounding **ifosfamide-related effects** (renal tubulopathy, and ifosfamide encephalopathy as a topic).
- **Accuracy trap 2 — secondary AML/MDS framing:** etoposide (topoisomerase-II inhibitor, used in IE) is a
  major driver of treatment-related leukemia, distinct from alkylator-driven MDS. PLAN lumps "alkylating-agent
  and radiation-related" 2nd malignancies and omits topo-II/etoposide. This is a Ewing-specific exposure the
  plan should name, or the cardiac/2nd-malignancy entries will be incomplete for the actual Ewing regimen.
- **Gap — radiation second sarcoma in-field:** correctly noted, but the surgery-vs-radiation *local-control*
  decision is the single most Ewing-distinctive late-effects fork (limb salvage vs amputation vs RT, growth
  arrest, in-field secondary sarcoma). Deserves to be elevated, not bundled under generic "orthopedic."

**C. Education-not-advice boundary — strong, with one residual risk.**
- Labeling, no-calculator non-goal, "applies only if you received…" framing, and seek-care routing are all
  well-handled and CI-enforced. This is the plan's best feature.
- **Residual risk:** the **"questions to ask your care team"** sets (task -016) and any dose-band content are
  the most likely places for advice-creep to slip past CI (a question can encode a recommendation). PLAN flags
  this in Open Questions but provides no concrete **rule** distinguishing an education prompt from a
  self-assessment/triage item. Needs an explicit, testable guideline + advocate sign-off criterion.

**D. Currency / guideline-update — directionally right, mechanically thin.**
- The `validUntil`/staleness fail-safe is a genuine differentiator. **But:** COG LTFU updates on a **~5-year
  cycle** (v5 2018 → v6 Oct 2023), and v6 made *substantive clinical reversals* — e.g., surveillance
  echocardiograms were **omitted for those at low cardiomyopathy risk**, and it **added** genetic-predisposition
  and novel-therapy surveillance ([COG v6 review](https://pmc.ncbi.nlm.nih.gov/articles/PMC12188901/)).
  A pure date-based `validUntil` would *not* have caught the v5→v6 reversal if a date were set generously.
  Recommend: pin `sourceVersion` to a **specific guideline edition**, and treat *any* new edition as a hard
  re-review trigger regardless of `validUntil` — plus subscribe to IGHG's rolling per-topic publication stream
  (IGHG publishes by domain on its own cadence, not a single version
  ([ighg.org recommendations](https://www.ighg.org/wp-content/uploads/2023/06/IGHG-Recommendations-June-2023.pdf))).
- **Gap:** PLAN treats COG/IGHG/ESMO/CCLG as parallel; it does not resolve that **IGHG harmonizes/supersedes**
  some COG positions and that the four bodies update asynchronously. "Spine guideline" is correctly raised as an
  open question but is a **blocking design decision**, not a deferrable one — content cannot be drafted coherently
  until it's settled.

**E. Psychosocial / AYA-specific needs — named but thin.**
- Listed, and routed to advocate review for harm-avoidance. Good. **Gap:** AYA survivorship has its own
  *harmonized* evidence base now — IGHG has issued recommendations on **education/employment outcomes** and
  **cancer-related fatigue** ([IGHG education/employment, Cancer/Wiley](https://acsjournals.onlinelibrary.wiley.com/doi/full/10.1002/cncr.34215))
  — which the plan's source list under-weights relative to organ-toxicity. AYA-specific issues (fertility
  decision regret, financial toxicity, insurance/employment, identity/transition, mental health) are the
  *differentiated* need and warrant a dedicated sourced module, not a sub-bullet.

**F. Source-license posture — correct and conservative.**
- NCI/PDQ public-domain (with PDQ trademark/no-endorsement caveat) is accurate. COG LTFU is freely
  downloadable but **copyrighted** by COG — cite-not-reproduce is the right call. Fact-vs-expression firewall +
  CI source-similarity check is appropriate. No error found. Minor: confirm **Health Links** reuse terms
  specifically (they may have different terms than the guideline PDF) before paraphrasing them closely.

**G. Clinical review gate — strong; one operational risk.**
- Dual blocking gate (oncologist + advocate, version-scoped, non-overridable) is excellent and correctly the
  Definition of Shipped. **Operational risk:** the *entire* project is gated on recruiting an unpaid
  credentialed pediatric/AYA late-effects specialist **and** a survivor-advocate **and** a distribution partner,
  with no partner yet secured and a hard mothball rule at ~2027-03-31. This is realistic honesty, but it means
  the most likely outcome on current resourcing is **M1 hold / mothball**. The reviewer-compensation question
  (funded lane for review hours, with COI firewall) is under-developed and is arguably the project's true
  critical path — it deserves elevation from an open question to a milestone-zero workstream.

**H. Metrics — outcome-centric (good), but some are weak/ungameable-but-unmeasurable.**
- "≥10 survivors report it helped" and "≥3 attested better-conversation outcomes" are honest but **very low
  bars** and depend entirely on a partner that may never materialize; there's no leading indicator before
  distribution. **Weak metric:** "LLM-judge faithfulness ≥ agreed threshold" — threshold is undefined and an
  LLM-judge grading LLM-drafted health claims is a known weak control without a labeled gold set + inter-rater
  agreement with the expert. Recommend defining the threshold, a human-labeled benchmark, and treating the
  LLM-judge as triage only (expert is the gate). **Missing metric:** time-to-re-review after a guideline
  update (the staleness fail-safe's actual effectiveness), and a copyright/source-similarity false-negative audit.

**I. Smaller gaps.**
- No explicit handling of **survivors who don't know their exposures** beyond "route to care team / exposure
  summary explainer." This is *the* core AYA problem (lost treatment summaries). A stronger answer: teach
  survivors how to **request their treatment summary** (and what fields matter), which competitors (Passport
  for Care, Journey Forward) operationalize. Currently only lightly addressed.
- **Ewing biology context** (EWSR1 fusion, typical age, bone vs extraosseous) is absent — not strictly needed
  for late-effects, but a small "what was Ewing / why this regimen" primer aids comprehension and is low-risk.
- No mention of **mobile/low-bandwidth/print** as a first-class channel until backlog (-025); for a global,
  equity-minded audience this should be nearer the core.

---

## 2. Competitive landscape

The space is **crowded with authoritative incumbents** — but almost none combine *Ewing-specific* +
*plain-language* + *exposure-linked* + *open/global* + *self-serve without a clinician account*. That four-way
intersection is the opening.

**1. COG Long-Term Follow-Up Guidelines + Health Links (the incumbent spine).**
What: the canonical exposure/risk-based surveillance compendium (v6.0, Oct 2023; 165 sections, 45 Health Links;
~5-yr update cycle) plus "Health Links" plain-language patient education on each topic. Publicly free at
[survivorshipguidelines.org](https://www.survivorshipguidelines.org/) and
[childrensoncologygroup.org/survivorship](https://childrensoncologygroup.org/survivorship/).
Strengths: gold-standard authority, exposure-based by design, already has a patient-education layer, free.
Weaknesses/gaps: **not cancer-specific** (organized by exposure/organ, not by "Ewing"); the survivor must
already know their exposures to navigate it; US-centric; not structured as a guided Ewing journey; Health Links
are topic sheets, not an integrated AYA-transition narrative; update cadence is slow (5-yr).

**2. Passport for Care (PFC) — the personalized clinical tool.**
What: free web-based clinical **decision-support** tool that generates a personalized treatment summary +
late-effects risk + LTFU plan from entered exposures, derived from COG LTFU (updated to v6, Nov 2023)
([cancersurvivor.passportforcare.org](https://cancersurvivor.passportforcare.org/en/);
[PFC implementation, PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC2790686/)). Recently joined forces with
Cancer SurvivorLink ([CHOA newsroom](https://www.choa.org/about-us/newsroom/passport-for-care-and-cancer-survivorlink-enhance-survivor-centered-care)).
Strengths: genuinely personalized, exposure-driven, COG-backed, includes tailored educational resources.
Weaknesses/gaps: **clinician/clinic-mediated** (a survivor aged out of a COG site may have no access);
generates a care plan (the thing PLAN deliberately won't do); requires the exposure data the AYA survivor often
lacks; not a browsable open library; not Ewing-narrative.

**3. NCI PDQ "Late Effects of Treatment for Childhood Cancer" + cancer.gov survivorship.**
What: authoritative, **public-domain** summaries (HP + patient versions) and survivorship/follow-up-care pages
([NCI late-effects PDQ](https://www.cancer.gov/types/childhood-cancers/late-effects-hp-pdq);
[NCI follow-up care](https://www.cancer.gov/about-cancer/coping/survivorship/follow-up-care)).
Strengths: most reusable license (public domain), authoritative, comprehensive.
Weaknesses/gaps: written largely for professionals (the patient version is denser than grade 6–8); not
Ewing-specific; not exposure-navigable as a tool; no AYA-transition product.

**4. St. Jude LIFE / After Completion of Therapy (ACT) Clinic.**
What: ACT clinic (est. 1984) delivers risk-based survivorship care + care plans; SJLIFE cohort (>6,200 enrolled)
is the research engine generating new late-effects evidence
([St. Jude ACT](https://www.stjude.org/treatment/survivorship/act-clinic.html);
[SJLIFE](https://www.stjude.org/content/sites/www/en_US/home/research/initiatives/cancer-survivorship-research/st-jude-life-study.html)).
Strengths: deepest evidence base, multidisciplinary model, drives the science.
Weaknesses/gaps: **institution-bound** (St. Jude patients); a research/clinical program, not an open
self-serve library; not Ewing-specific patient education.

**5. IGHG — International Late Effects of Childhood Cancer Guideline Harmonization Group.**
What: harmonizes the world's surveillance guidelines into consensus recommendations by topic (cardiomyopathy,
breast, pulmonary, fatigue, education/employment, etc.), published per-domain
([ighg.org](https://www.ighg.org/wp-content/uploads/2023/06/IGHG-Recommendations-June-2023.pdf);
[IGHG cardiomyopathy, Lancet Onc](https://www.thelancet.com/journals/lanonc/article/PIIS1470-2045(23)00012-8/abstract)).
Strengths: international/consensus (resolves US-vs-EU divergence), strong evidence grading, the natural "spine"
where schedules differ.
Weaknesses/gaps: clinician-facing journal articles; copyrighted; no patient-facing plain-language product; no
Ewing view.

**6. Livestrong (incl. SMART ALACC + OncoLife).**
What: survivorship-care-plan generators — OncoLife (adult, with UPenn) and **SMART ALACC for childhood cancer
survivors** — plus healthy-living-after-treatment content
([Livestrong SCP](https://www.livestrong.org/we-can-help/healthy-living-after-treatment/your-survivorship-care-plan)).
Strengths: consumer-friendly, free, generates a personalized plan incl. late-effects.
Weaknesses/gaps: general (not Ewing); plan-generator (not a sourced education library); variable provenance
transparency; not exposure-dose granular.

**7. Macmillan / Cancer Research UK (and ACS / Cancer.Net).**
What: large charities with strong plain-language late-effects content; ACS/Cancer.Net has an explicit
**"After Treatment for Ewing Sarcoma"** survivorship page
([Macmillan late effects](https://www.macmillan.org.uk/cancer-information-and-support/after-treatment/late-effects-of-treatment);
[Cancer.Net Ewing survivorship](https://www.cancer.net/cancer-types/ewing-sarcoma-childhood-and-adolescence/survivorship)).
Strengths: excellent readability, trusted brands, Cancer.Net is Ewing-tagged.
Weaknesses/gaps: **adult-skewed / UK health-system-specific** (Macmillan/CRUK); not exposure-linked at
dose-band granularity; not open-licensed for derivative reuse; the Ewing pages are thin overview, not a
late-effects-by-exposure library.

**8. National Coalition for Cancer Survivorship (now "Cancer Nation") + Journey Forward.**
What: oldest survivor-led advocacy org; Cancer Survival Toolbox (audio), Survivorship Checklist, and
**Journey Forward** (treatment-summary + follow-up-plan tooling)
([canceradvocacy.org](https://canceradvocacy.org/);
[NCCS survivorship checklist](https://canceradvocacy.org/resources/survivorship-checklist/)).
Strengths: advocacy credibility, self-advocacy skills content, treatment-summary tooling.
Weaknesses/gaps: general adult survivorship; not pediatric/AYA Ewing; not exposure-linked education.

**9. Sarcoma/AYA-specific orgs (adjacent, partnership targets more than competitors).**
Ewing Sarcoma Institute ([ewingsarcoma.org](https://www.ewingsarcoma.org/)) and Sarcoma Foundation of America
(research/awareness focus, thin on structured survivorship); AYA communities — **Stupid Cancer**, **Cactus
Cancer Society**, Froedtert/CHLA/Angie Fowler AYA programs; INSPIRE-AYA (interactive AYA survivorship program).
Strengths: real survivor communities and distribution reach; AYA-native voice.
Weaknesses/gaps: little rigorous, sourced, exposure-linked late-effects content — they are **distribution
partners + voice**, and they have the audience this project lacks.

**Net read:** authority is saturated (COG/NCI/IGHG/St. Jude) and personalization-tools exist (PFC, Livestrong,
Journey Forward), but they are **either clinician-mediated, not cancer-specific, not open-licensed, or not
plain-language at grade 6–8.** No incumbent owns "**Ewing-specific, exposure-explained, grade-6–8, open
(CC-BY), self-serve, globally accessible, harmonized across guidelines.**"

---

## 3. Gaps we can fill

1. **Ewing-specific synthesis.** Every incumbent is either all-cancers (COG, NCI, Livestrong) or thin-overview
   for Ewing (Cancer.Net). No one maps **the actual Ewing regimen (VDC/IE: vincristine, doxorubicin,
   cyclophosphamide, ifosfamide, etoposide ± surgery/RT local control)** to its specific late-effect profile in
   plain language. This is the core unfilled niche.
2. **Exposure → late-effect explanation, not a care plan.** PFC/Livestrong *generate plans* (and need exposure
   data the AYA lacks). We instead **explain why each exposure class drives each late effect and what the
   guidelines recommend watching for** — useful even before the survivor has their exposure summary, and it
   teaches them what to go retrieve.
3. **The "I don't know my exposures" on-ramp.** Concretely teach survivors to obtain a treatment summary, what
   fields matter (cumulative anthracycline dose, RT field/dose, agents), and how to read it — bridging the gap
   that breaks LTFU at the pediatric→adult handoff.
4. **Harmonized, health-system-neutral view.** Reconcile COG (US) vs IGHG (international) vs ESMO/CCLG (EU/UK)
   into a "what the consensus recommends, and where systems differ" view — something no single body's
   patient-facing material does (each presents its own schedule as the answer).
5. **Truly open + globally accessible.** CC-BY-4.0, static, low-bandwidth/print, translation-ready. COG Health
   Links and Macmillan are free-to-read but not openly licensed for derivative reuse/translation; PFC is
   account/clinic-gated. Open licensing lets advocacy orgs and clinics worldwide adopt/translate it.
6. **Grade 6–8 + WCAG 2.2 AA as a hard gate.** Most authoritative late-effects content (NCI PDQ patient version,
   IGHG papers) reads well above grade 8. Enforced readability is a measurable quality others don't gate on.
7. **AYA-native framing of psychosocial/fertility/employment** as first-class, sourced topics (leveraging
   IGHG's education/employment + fatigue harmonized recs) — under-served by organ-toxicity-centric incumbents.
8. **Provenance transparency.** Per-assertion citation + version + "how we made this" exceeds the transparency
   of consumer SCP generators, building trust for a vulnerable audience.

---

## 4. Differentiators to win

1. **The only open, Ewing-specific, exposure-explained, grade-6–8 late-effects library** — the four-way
   intersection no incumbent occupies (single strongest differentiator).
2. **Education *about* exposures, not a personalized calculator** — sidesteps the regulatory/advice risk that
   constrains PFC-style tools while still being exposure-relevant, and works without the survivor's data.
3. **Harmonized cross-guideline view** (IGHG-led consensus + named divergences) instead of one country's
   schedule — uniquely useful to a global/diaspora audience.
4. **Safety/provenance as enforced code** — dual blocking clinical+advocate gate, no-source-no-claim CI,
   fact-vs-expression firewall, staleness fail-safe tied to guideline editions. A trust posture that exceeds
   typical patient-education sites and is defensible for HIGH-risk content.
5. **Open license + translation-ready + low-bandwidth** — adoptable by sarcoma/AYA orgs and clinics anywhere,
   turning potential competitors (Ewing Sarcoma Institute, Stupid Cancer, Cactus, survivorship clinics) into
   distributors.
6. **Beneficiary-defined success** (reviewed content reaching real survivors + attested "better conversation"),
   not pageviews — aligns with Hee-Lee Oss outcomes-over-merges ethos and with the dual review gate.

---

## 5. Claude API leverage

**Where Claude clearly helps (assistive, human-gated):**
1. **Exposure-based synthesis with per-assertion citations.** Claude drafts plain-language late-effect entries
   from *retrieved, allowlisted* guideline text (COG/IGHG/NCI), emitting each claim with its `sourceRef`
   (body/document/section/version) — a retrieval-grounded, citation-first drafting loop that directly serves the
   no-source-no-claim schema. Use Claude's strength at structured extraction to populate the `assertions[]` +
   `provenance[]` records, not just prose.
2. **Plain-language rewriting to a target reading grade.** Claude rewrites clinician-grade guideline language to
   grade 6–8 while preserving the cited fact, then self-checks readability — the single highest-leverage,
   lowest-risk use, addressing the gap that NCI PDQ / IGHG papers read above grade 8.
3. **"Questions for your follow-up visit" generation.** From a sourced late-effect entry, Claude drafts
   education-only prompt lists ("ask whether your treatment summary records your total anthracycline dose")
   — bounded to non-self-assessment phrasing, advocate-reviewed.
4. **Non-clinical, exposure-class summaries** ("what applies if you received an anthracycline") that explain
   *categories* without ever computing an individual's risk.
5. **Faithfulness triage (LLM-as-judge) + source-similarity pre-screen.** Claude flags drift between a claim and
   its cited source, and flags passages too close to copyrighted text — as *triage that routes to the expert*,
   never as the gate.
6. **Cross-guideline reconciliation drafting.** Claude surfaces where COG vs IGHG vs ESMO/CCLG diverge on a
   schedule, for the human to verify — accelerating the health-system-neutrality work.
7. **Staleness/update assistance.** On a new guideline edition, Claude diffs old vs new recommendations to
   propose which assertions need re-review (e.g., it would surface v6's low-risk-echo omission for human
   confirmation).

**Where Claude must NOT decide (hard lines, enforced by the dual gate + CI):**
- **No medical advice and no individualized screening recommendation** — ever. Claude may explain what
  guidelines recommend *in general by exposure class*; it may not tell a person what *they* should do.
- **No unsourced or fabricated facts/citations.** Every claim must resolve to a real allowlisted source;
  hallucinated facts or citations fail the citation-coverage gate. Claude's output is a *draft*, not truth.
- **Claude is not the faithfulness gate.** LLM-judge is triage only; a credentialed oncologist signs off on
  clinical accuracy and a survivor-advocate on harm-avoidance — neither overridable by the model or maintainer.
- **No personalized risk scores/calculators** (explicit non-goal) — Claude must not be wired into any per-user
  data intake.
- **No reproduction of protected expression** — Claude synthesizes facts in original words; verbatim
  guideline text/tables/figures are blocked by the source-similarity gate.
- **No controlled-access/identifiable data** ever enters the prompt context (open-access/aggregate only).

---

## 6. Ten concrete optimizations

1. **Settle the "spine guideline" now (IGHG-harmonized as default, COG/ESMO/CCLG as named divergences).**
   Promote from Open Question to an M0 design decision — content cannot be drafted faithfully until it's fixed.
2. **Pin provenance to guideline *edition*, and make any new edition a hard re-review trigger** independent of
   `validUntil` (the v5→v6 cardiac-surveillance reversal would otherwise slip). Subscribe to IGHG's per-domain
   publication stream, not just COG's 5-year cycle.
3. **Add explicit, sourced dose-band vocabulary to the schema** (anthracycline cumulative-dose tiers, RT
   ≥X Gy field thresholds) — with a hard rule that bands are *educational categories*, never per-user risk.
4. **Fix the Ewing-regimen fidelity:** name **etoposide/topoisomerase-II → treatment-related leukemia**;
   demote **ototoxicity/platinum** to conditional (not standard VDC/IE); add **ifosfamide encephalopathy**;
   elevate the **surgery-vs-radiation local-control** fork as its own MSK module.
5. **Define the faithfulness eval rigorously:** a human-labeled gold set, a numeric threshold, inter-rater
   agreement with the expert, and LLM-judge-as-triage-only. Replace "≥ agreed threshold" with a real number.
6. **Write a testable "education-prompt vs self-assessment" rule** for the questions sets, enforced in CI +
   advocate sign-off, closing the most likely advice-creep leak.
7. **Build the "get your treatment summary" on-ramp early** (what to request, which fields matter, how to read
   it) — converts the AYA's biggest gap (lost exposure data) into an actionable, low-risk first deliverable.
8. **Make print/low-bandwidth/offline a core channel, not backlog** — equity for a global audience; a CC-BY
   printable handout pack derived from dual-signed content.
9. **Elevate reviewer compensation + COI firewall to an M0 workstream.** The unpaid-expert dependency is the
   true critical path; design a funded-lane-for-review-hours option (hard cap, independence preserved) before
   the mothball clock runs.
10. **Add leading-indicator metrics before distribution:** faithfulness pass-rate on the gold set,
    time-to-re-review after a simulated update, readability distribution, and a source-similarity
    false-negative audit — so quality is measurable before a partner exists.

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same engine, adjacent content — strong reuse):**
- **`ewing-family-guide`** — a diagnosis/treatment plain-language companion (what Ewing is, the VDC/IE regimen,
  local control), the upstream sibling to this downstream survivorship library; shared schema/provenance/gates.
- **`survivorship-resources`** — a curated, sourced directory of vetted survivorship programs/clinics/orgs
  (COG sites, AYA programs, Ewing Sarcoma Institute, Stupid Cancer, Cactus) the library routes survivors to.
- **`question-prompt-lists`** — generalize the "questions for your follow-up visit" generator into a reusable,
  education-only, advocate-reviewed component across conditions.
- **`nutrition-during-treatment`** — adjacent supportive-care education sharing the same no-advice + provenance
  architecture (note higher advice-creep risk; same gates apply).

**Perpendicular (bigger bets):**
- **Generalized exposure-based survivorship engine across cancers.** The schema (exposure → late effect →
  sourced surveillance, harmonized across guidelines, grade-6–8, open) is **cancer-agnostic**. Ewing is the
  vertical slice; the platform could template every COG LTFU exposure into open patient education — an open,
  plain-language, multi-guideline complement to Passport for Care that *no one* currently offers openly.
- **Guideline-currency service.** The edition-pinned staleness fail-safe + Claude-assisted guideline-diff is a
  reusable capability ("tell me which patient-education assertions a new COG/IGHG edition invalidates") valuable
  to any patient-education publisher.
- **Open translation layer.** Translation-ready + per-language reviewer gating could make this the first
  openly-licensed, multilingual childhood/AYA survivorship education set — high impact for global/diaspora
  survivors underserved by US/UK-centric incumbents.

**Partnerships:** COG / survivorshipguidelines.org (alignment + possible Health Links cross-link), IGHG
(consensus alignment), Passport for Care / Cancer SurvivorLink (complementary: they personalize behind a clinic,
we educate openly), St. Jude survivorship, and AYA/sarcoma distributors (Ewing Sarcoma Institute, Stupid Cancer,
Cactus Cancer Society, INSPIRE-AYA) for last-mile reach and survivor voice.

---

## 8. Open questions for the maintainer

1. **Spine guideline:** confirm IGHG-harmonized as default with COG/ESMO/CCLG divergences named — and accept
   that this blocks content drafting until decided?
2. **Ewing-regimen fidelity:** will you add etoposide/topo-II → leukemia, demote platinum-ototoxicity to
   conditional, and elevate surgery-vs-RT local control? (Needs clinical-reviewer confirmation.)
3. **Reviewer compensation:** is a funded-lane-for-review-hours (hard cap, COI firewall) on the table, given
   the unpaid-expert dependency is the likely make-or-break? Should it be an M0 workstream?
4. **Relationship to COG Health Links:** position as complementary (Ewing-integrated, harmonized, open) — or
   risk duplicating free material? Will you seek COG alignment/cross-linking rather than parallel build?
5. **Dose-band granularity:** how granular can exposure bands be before they read as individualized risk? Where
   exactly is the schema's hard line?
6. **Distribution realism:** if the mothball clock (~2027-03-31) is the likely outcome, should partner
   recruitment (e.g., Ewing Sarcoma Institute, an AYA org) start *before* M2 content rather than after?
7. **"Questions to ask" boundary:** what is the concrete, testable rule separating an education prompt from a
   self-assessment/triage item?
8. **Faithfulness threshold + gold set:** who builds the human-labeled benchmark, and what numeric pass-rate
   gates publication?
9. **Treatment-summary on-ramp:** acceptable to make "how to get and read your treatment summary" an early,
   low-risk deliverable (it's process guidance, not clinical advice)?
