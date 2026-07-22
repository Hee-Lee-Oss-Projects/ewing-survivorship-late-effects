# Ewing-Survivorship-Late-Effects — PLAN.md

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

An open, plain-language **survivorship / late-effects resource library** for survivors of **Ewing
sarcoma**, focused on the **pediatric → adolescent-and-young-adult (AYA)** transition. It turns the
recommendations of vetted bodies (NCI/PDQ, Children's Oncology Group [COG] Long-Term Follow-Up
Guidelines, ESMO, CCLG, and the International Guideline Harmonization Group [IGHG]) into clear,
sourced, education-only material that helps survivors and their families understand *what late
effects can follow Ewing treatment, why, and what survivorship care those bodies recommend* — so
they can have better-informed conversations with their own care team.

It is **not** medical advice, **not** a diagnosis or risk calculator, and **not** a substitute for a
survivorship clinic. Every assertion is sourced; every page is labeled **"Informational, not medical
advice — consult your care team"**; and **no content ships without dual sign-off from a credentialed
pediatric/AYA oncologist *and* a patient advocate.** This is a **HIGH risk-tier** project under
`docs/good-deed-definition.md`.

---

## Executive summary

Ewing sarcoma is a rare bone-and-soft-tissue cancer that disproportionately strikes children,
adolescents, and young adults. Survival has improved markedly, which means a growing population of
survivors now lives for decades with the **late effects** of intensive therapy — anthracycline
cardiotoxicity, alkylator- and radiation-related second cancers, gonadotoxicity/infertility,
ifosfamide nephrotoxicity, ototoxicity, vincristine neuropathy, and the orthopedic, growth,
neurocognitive, and psychosocial consequences of surgery and radiation to a growing body. The
late-effect profile is **directly tied to the specific treatment a person received** (which drugs,
cumulative doses, radiation field/dose, and type of local control). Authoritative survivorship
guidance exists — chiefly the **COG Long-Term Follow-Up (LTFU) Guidelines**, NCI's PDQ summaries,
ESMO and CCLG guidance, and the **IGHG** harmonized recommendations — but it is written for
clinicians, fragmented across documents and health systems, and largely inaccessible to a 19-year-old
survivor aging out of pediatric care.

This project builds a small, rigorously sourced, **education-only** library that translates that
guidance into plain language for survivors and families, organized around the **pediatric → AYA
transition** (the point at which many survivors fall out of structured follow-up). The deliverable is
open content (CC-BY-4.0) plus a lightweight, agent-neutral build/validation toolchain (MIT).

The single most important design fact is that **this is health information for a vulnerable
population, so safety and provenance lead the architecture, not the features.** Three properties are
hard product requirements, built first and tested as safety-critical, not bolted on:

1. **A dual, blocking clinical+lived-experience review gate.** No page reaches a real survivor until
   a **credentialed pediatric/AYA oncologist (or late-effects specialist)** has signed off on
   clinical accuracy *and* a **patient advocate / survivor reviewer** has signed off on tone, framing,
   and harm-avoidance. Neither sign-off alone is sufficient. This is the project's Definition of
   Shipped gate and cannot be waived by the maintainer.
2. **Per-assertion provenance with a no-source-no-claim rule.** Every factual statement is backed by
   a citation to a vetted body, with the guideline, section, version/date, retrieval date, evidence
   level where stated, and a recorded **license/legal status**. A page with an unsourced clinical
   claim fails the build.
3. **Cancer data guardrails.** Only **open-access / aggregate / de-identified** sources are used.
   **Controlled-access data (dbGaP, EGA, individual-level biobanks) and any identifiable patient
   data are out of scope.** Each source's reuse terms are verified and recorded before its content
   ships. (See *Data, licensing & compliance*, which leads with these guardrails.)

**Honesty note: no partner organization, clinical reviewer, patient advocate, or last-mile steward
is yet secured.** Every delivery-dependent task is marked `TO BE SECURED` with `verifiedNeed: false`.
The project is **not** "shipped" on merge — it ships only when reviewed content reaches real
survivors/families through a partner (a survivorship clinic, a sarcoma/AYA advocacy organization, or
an oncology program), with both sign-offs recorded.

**Dated partner-acquisition plan and build-vs-mothball decision rule.** Outreach is time-boxed
against the build, not open-ended: by **2026-08-31** a credentialed pediatric/AYA oncologist reviewer
and a patient-advocate reviewer are in active conversation and ≥ 2 candidate distribution partners
(sarcoma/AYA advocacy org or survivorship clinic) are engaged; by **2026-10-31** at least one
clinical reviewer **and** one advocate reviewer are secured (this gates all M2 content); by
**2026-12-31** a last-mile distribution partner/steward is secured (gates M5). **Decision rule:** if
no credentialed clinical reviewer **and** advocate reviewer are secured by the M2 entry date, **no
patient-facing content is drafted or published** — the project holds at M1 (toolchain + provenance +
licensing) and produces only an internal, clearly-watermarked exemplar for reviewer recruitment. If
no distribution partner is secured by **2027-03-31**, the project does **not** publish to the open web
blindly; it either (a) **pivots** the last-mile channel (hand the reviewed library to an existing
trusted patient-education publisher as a contribution) or (b) **mothballs** to maintenance-only, with
the decision recorded in governance. Publishing high-risk health content to no vetted channel and no
beneficiary is explicitly **not** an acceptable outcome.

---

## Problem & beneficiaries

**Who is helped (directly):** survivors of Ewing sarcoma, especially those **transitioning from
pediatric oncology follow-up into adolescent/young-adult and adult care** (roughly ages 15–39), and
their **parents and caregivers**. This is the life stage where structured long-term follow-up most
often breaks down: the survivor leaves the pediatric center, may not have a survivorship care plan in
hand, may not know which exposures they received, and frequently does not know what surveillance the
guidelines recommend for *them*.

**Who is helped (ultimately):** the wider Ewing/sarcoma and childhood-cancer survivor community, the
clinicians and survivorship programs who can point patients to a trustworthy plain-language resource,
and advocacy organizations that need vetted educational material they did not have to author from
scratch.

**The need.** Ewing therapy is intensive and multimodal (multi-agent chemotherapy including
anthracyclines, alkylating agents, and vincristine; surgery and/or radiation for local control), and
its late effects are well-documented but exposure-dependent and clinician-facing. Survivors
routinely report: not understanding why a given screening matters, losing their treatment-exposure
summary, no clear "what now?" at the pediatric→adult handoff, and either over-worrying or
under-engaging with follow-up. Authoritative survivorship guidance (COG LTFU, NCI PDQ, IGHG, ESMO,
CCLG) exists but is fragmented, written for professionals, and split across health systems with
**different surveillance schedules** — so a survivor cannot easily learn what *the consensus
recommends* in language they can use.

**Verified need / partner: TO BE SECURED.** No specific survivorship clinic, advocacy organization,
clinical reviewer, or patient-advocate reviewer has yet agreed to co-develop, review, or distribute
the library. Target partner profiles: a **pediatric/AYA survivorship program** (e.g., a long-term
follow-up clinic), a **sarcoma or AYA-cancer advocacy/foundation** with a survivor community, and
credentialed **late-effects/survivorship clinicians** plus **survivor-advocate reviewers**. Until
secured, the project builds the toolchain, the provenance/licensing layer, and **one** illustrative
late-effect exemplar (internal, watermarked, not published) for reviewer recruitment, and marks all
delivery/adoption work `TO BE SECURED`. Outreach is **dated** (see executive summary), with a
build-vs-mothball/pivot rule if dates slip — high-risk health content is never shipped to no
reviewer and no beneficiary.

---

## Goals and non-goals

**Goals**

- Produce an open, plain-language survivorship/late-effects library for Ewing survivors, organized
  around the pediatric→AYA transition, that is **education only** and **fully sourced** to vetted
  bodies.
- Make every assertion traceable: a no-source-no-claim provenance model with guideline, section,
  version, retrieval date, evidence level, and license status on each claim.
- Key content to **treatment exposures** (which drugs/doses, radiation field, surgery type) so it is
  honest that "what applies to you depends on the treatment you received," without ever computing an
  individual's risk.
- Ship every page behind a **dual blocking review gate**: credentialed pediatric/AYA oncologist
  (clinical accuracy) **and** patient advocate/survivor (tone, framing, harm-avoidance).
- Meet plain-language (target reading grade 6–8), accessibility (WCAG 2.2 AA), and
  translation-ready structural standards.
- Deliver the reviewed library to real survivors/families through a vetted partner, and track that
  it actually reached and helped them — not that pages were merged.

**Non-goals**

- **No medical advice, diagnosis, prognosis, dosing, or treatment recommendations.**
- **No personalized or individual risk score / calculator.** General, guideline-grounded education
  only; we never tell an individual their risk.
- Not a clinical-trial finder, not a symptom checker, not a substitute for a survivorship clinic or
  a survivorship care plan authored by the survivor's own team.
- Not a research data project: no controlled-access data, no individual-level patient data, no
  re-identification, no novel epidemiology.
- Not a verbatim re-publication of copyrighted guidelines (COG/ESMO/CCLG/IGHG text, tables, or
  figures). We synthesize *facts* in original plain language and cite the source.
- Not health-system-specific dogma: where surveillance schedules differ by guideline/country, the
  content says so rather than implying one system is "the" answer.
- Not comprehensive of every rare late effect at launch — depth and verified accuracy on the core,
  high-burden Ewing late effects first; breadth later, and never breadth without review.

---

## Success metrics (outcomes)

Outcome-centric and beneficiary-first. Vanity metrics (pageviews, sessions) are explicitly **not**
success.

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Dual sign-off before any page ships | none | **100%** of published pages have recorded oncologist **and** advocate sign-off, version-scoped | Governance/reviewers ledger; CI publish gate |
| Assertions carrying a valid source citation | none | **100%** (no-source-no-claim) | Citation-coverage test in CI |
| Source-faithfulness (plain-language claim matches its cited source) | n/a | **100%** of sampled assertions judged faithful by expert; LLM-judge faithfulness ≥ agreed threshold with expert spot-check | Faithfulness eval + reviewer audit |
| Copyrighted-text reuse (verbatim guideline text/tables/figures) | n/a | **0** instances; similarity check below threshold | Source-similarity check in CI + reviewer review |
| Controlled-access / identifiable-data sources used | n/a | **0** (hard gate) | Source allowlist + provenance audit |
| "Informational, not medical advice" labeling coverage | n/a | **100%** of pages | Build-time label test |
| Plain-language reading level | n/a | core pages at **grade 6–8** target; advocate-confirmed | Readability metric + advocate review |
| Accessibility | n/a | core pages meet **WCAG 2.2 AA** | Automated + manual a11y audit |
| Stale-content containment | n/a | **0** assertions served past their guideline `validUntil` without auto-flag/withhold + re-sign-off | Staleness test against `sourceVersion`/`validUntil` |
| Reached real beneficiaries via a partner | 0 | library distributed through ≥ 1 vetted partner to its survivor community | Partner/steward attestation |
| Survivor/caregiver-reported usefulness | 0 | ≥ 10 survivors/caregivers report the material helped them prepare for or understand a follow-up conversation (anonymous, opt-in) | Anonymous feedback (no PII) + partner report |
| Documented "better conversation" outcomes | 0 | ≥ 3 attested instances of a survivor using the library to prepare questions / understand recommended surveillance | Partner/steward attested log (de-identified) |

The **defining success outcome** (Definition of Shipped): reviewed, dual-signed-off content reaches
real survivors/families through a vetted partner and demonstrably helps them understand or prepare
for their survivorship care — with clinical accuracy and harm-avoidance independently verified, every
assertion sourced, and the cancer data guardrails upheld.

---

## Scope

**In scope**

- A curated set of **late-effect topics** relevant to Ewing therapy, each keyed to the treatment
  exposure(s) that drive it:
  - Anthracycline (e.g., doxorubicin) **cardiotoxicity** and recommended cardiac surveillance.
  - Alkylating-agent (cyclophosphamide, ifosfamide) and radiation-related **second
    malignant neoplasms** (e.g., secondary AML/MDS, sarcomas in the radiation field).
  - **Gonadotoxicity / fertility** effects of alkylators (and fertility-preservation awareness).
  - **Ifosfamide nephrotoxicity** (tubulopathy/Fanconi-type) and renal surveillance.
  - **Ototoxicity** (where platinum/relevant exposures apply) and hearing surveillance.
  - **Vincristine peripheral neuropathy** and long-term neuromuscular effects.
  - **Orthopedic / musculoskeletal / growth** effects of surgery (limb salvage, amputation,
    endoprosthesis) and radiation to growing bone (length discrepancy, scoliosis, function).
  - **Neurocognitive and psychosocial** late effects and AYA mental-health/quality-of-life.
  - Pulmonary and other organ effects where Ewing-relevant exposures apply.
- A **pediatric → AYA transition** module: what a survivorship care plan is, the value of a
  treatment-exposure summary, transitioning from pediatric to adult/AYA survivorship care, and
  **"questions to ask your care team"** sets.
- A **provenance + licensing** layer (per-assertion sources, license status, staleness fail-safe).
- A lightweight, agent-neutral **build/validation toolchain** (citation-coverage check, label check,
  readability check, source-similarity check, staleness check, accessibility check) and a static,
  translation-ready content format.
- Dual-audience framing (survivor-facing and caregiver-facing; AYA-appropriate voice).

**Out of scope (explicitly will NOT do)**

- Any **medical advice, diagnosis, prognosis, dosing, individualized risk score, or treatment
  recommendation.**
- **Controlled-access data (dbGaP, EGA, individual-level biobanks) and ANY identifiable patient
  data** — out of scope entirely; no IRB/authorized-access workflow is in scope.
- Verbatim reproduction of copyrighted guideline text, tables, or figures (COG/ESMO/CCLG/IGHG and
  journal content). We use facts + citation + original plain-language expression only.
- Symptom checkers, triage tools, clinical-trial matching, or any interactive tool that could be
  read as individualized clinical guidance.
- Collecting patient data of any kind. No accounts, no health data intake, no analytics that profile
  individuals; feedback is anonymous and optional.
- Claiming completeness or endorsing one country's surveillance schedule as universal.

When a request or contribution drifts into the out-of-scope set (e.g., "what should *I* do about my
heart?"), the content holds the line: it explains what the **guidelines recommend in general**,
labels itself education-only, and **directs the reader to their care team / survivorship clinic** —
never an individualized answer.

---

## Solution approach & architecture

This is primarily a **content + data** project with a thin software toolchain; the "architecture" is
a content pipeline with safety and provenance enforced as code.

**Content model (the core artifact).** Each topic is a structured **Late-Effect Entry** with a
machine-checkable schema:

- `id`, `title` (plain-language), `audience` (`survivor` | `caregiver` | `both`), `ayaVoice` (bool).
- `exposures[]` — the treatment exposures that drive this late effect (e.g., `anthracycline`,
  `ifosfamide`, `cyclophosphamide`, `vincristine`, `radiation:field+dose-band`, `surgery:type`),
  with an explicit **"this applies to you only if you received…"** framing.
- `sections[]` — plain-language blocks: *what it is*, *why it can happen after Ewing treatment*,
  *what the guidelines recommend watching for / surveillance*, *questions to ask your care team*,
  *red-flag "seek care" notes* where relevant.
- `assertions[]` — every clinical statement carries one or more `sourceRef`s (see provenance).
- `provenance[]` — `{ body, document, section, version, retrievedAt, evidenceLevel?, url,
  licenseStatus }` per `Source`.
- `labels` — mandatory `"Informational, not medical advice — consult your care team"`; `validUntil`
  derived from the governing guideline's review cadence.
- `review` — `{ clinicalSignoff: {reviewer, version, date}, advocateSignoff: {reviewer, version,
  date} }` — **both required to publish**.

**Pipeline.**
1. **Source vetting** → an allowlist of vetted bodies (NCI/PDQ, COG LTFU, IGHG, ESMO, CCLG, plus
   open-access/aggregate published statistics) with each source's reuse terms verified and recorded.
2. **Drafting** (AI-assisted synthesis, human-owned) → plain-language entries expressing *facts* from
   the sources in original words, each assertion linked to a `Source`.
3. **Automated gates (CI)** → citation-coverage (no-source-no-claim), mandatory-label check,
   source-similarity check (no verbatim copyrighted text), readability check, accessibility check,
   staleness check, and the open-access-only source allowlist check.
4. **Faithfulness eval** → an LLM-judge + expert spot-check that each plain-language assertion is
   faithful to its cited source (no drift, no invented specificity).
5. **Dual human review gate (blocking)** → oncologist clinical sign-off **and** advocate
   tone/harm-avoidance sign-off, both version-scoped and recorded.
6. **Publish** → static, accessible, translation-ready output, only for entries that pass all gates.

**Tech stack.** TypeScript, ESM, pnpm workspaces (consistent with Hee-Lee Oss conventions). Content as
structured Markdown/MDX or JSON validated by a JSON Schema; a static-site generator for publication;
validation scripts run in CI (`pnpm build && pnpm test && pnpm lint`). Any AI drafting/eval calls go
through a thin, provider-neutral LLM client (Claude as the reasoning resource, per the Claude API
skill), keeping the content/toolchain agent-neutral per `CLAUDE.md`. No database of patient data
exists by design.

**Key decisions.**
- Safety + provenance are first-class, tested gates, not documentation.
- Facts-not-expression: synthesize and cite; never reproduce copyrighted guideline text.
- Exposure-keyed, never personalized: content is general education tied to exposure classes, with no
  individual risk computation.
- One vertical-slice exemplar end-to-end through the full gate **before** scaling content.
- Translation-ready structure now; actual translations are gated per-language by a qualified reviewer
  (backlog).

---

## Data, licensing & compliance

**This section leads with the binding cancer guardrails. They are non-negotiable and gate everything
below.**

**1) Cancer data guardrails (binding).**
- **Open-access / aggregate / de-identified sources ONLY.** Permitted inputs: NCI PDQ summaries,
  published clinical-practice and long-term-follow-up guidelines (COG, ESMO, CCLG), IGHG harmonized
  recommendations, and **open-access or aggregate, de-identified** published statistics (e.g.,
  population-level incidence/late-effect frequencies from open-access literature or aggregate public
  reports).
- **Out of scope entirely:** controlled-access data (**dbGaP, EGA**), individual-level biobanks, and
  **ANY identifiable patient data**. No authorized-access/IRB workflow is in scope; if a fact would
  require such data, it is not used. A **source allowlist** plus a provenance audit enforce this in
  CI — a provenance record pointing at a controlled-access or individual-level source fails the gate.
- **Verify each source's license/reuse terms before its content ships**, and record the result.

**2) Source licensing — the fact-vs-expression firewall (critical).** The vetted survivorship bodies
publish under a range of terms, and most are **not** openly licensed for derivative redistribution:
- **NCI / PDQ:** U.S. government work; PDQ summaries are generally **public domain** and reusable with
  attribution (PDQ is a registered trademark; do not imply NCI endorsement). Most permissive source.
- **COG Long-Term Follow-Up Guidelines:** freely downloadable but **copyrighted by the Children's
  Oncology Group**, typically for personal/clinical/educational use — **not** a grant to redistribute
  derivative text. We **cite** them and express their *recommendations as facts in our own words*; we
  do **not** reproduce their text, tables, or figures without written permission.
- **ESMO, CCLG, IGHG and journal-published guidelines:** copyrighted (often by the society or its
  publisher). Same rule: **cite and synthesize facts; do not reproduce protected expression.**
- **Operating principle:** facts and ideas are not copyrightable; specific expression, tables, and
  figures are. Our output is **original plain-language synthesis of guideline facts, attributed to
  the source**. A **source-similarity check** in CI flags any passage too close to source text, and
  reviewers confirm no protected expression was copied. Where reproducing a specific table/figure
  would genuinely help survivors, we **seek explicit permission** and record it — we do not assume.

**3) Provenance model (no-source-no-claim).** Every clinical assertion is backed by ≥ 1 `Source`
record: `{ body, document, section/locator, version/edition, retrievedAt, evidenceLevel?, url,
licenseStatus }`. A page with an unsourced clinical claim **fails the citation-coverage test**. The
public output shows readable citations and a "sources & how we made this" page.

**4) Staleness fail-safe.** Each `Source` carries a `version`/edition and a `validUntil` derived from
that body's review cadence (guidelines are revised; e.g., COG LTFU versions update). At publish/serve
time, an assertion whose source is **past `validUntil`** is **auto-flagged or withheld** until it is
re-verified against the current version **and re-signed-off** by both reviewers. A guideline update
is therefore a **visible, gated event**, not silent staleness — a known, dangerous failure mode for
health content.

**5) Output licensing.** Our original content/synthesis: **CC-BY-4.0** (preserving attribution to the
underlying vetted sources). Toolchain code: **MIT**. Docs: CC-BY-4.0. (CC-BY applies to *our*
expression; it does not and cannot relicense the upstream copyrighted guidelines, which remain
cited, not redistributed.)

**6) Privacy / PII stance (conservative).** The library **collects no patient data** — no accounts,
no health intake, no individual risk inputs. There is **nothing to re-identify**. Optional feedback
is **anonymous** with no PII and no profiling analytics. No secrets, tokens, or PII are written to
logs, receipts, or committed files (Hee-Lee Oss rule). The "no individual data" stance is a design
constraint, not a setting.

**7) No-medical-advice labeling & attribution.** Every page carries **"Informational, not medical
advice — consult your care team."** Citations attribute primary sources; redistribution preserves
CC-BY attribution. Reviewers are credited (with consent, version-scoped) in a reviewers ledger.

---

## Quality, review & risk gates

**This section leads with the binding requirement: for this HIGH-risk, patient-facing project, the
oncologist + patient-advocate review is an explicit BLOCKING gate — no deed ships without it.**

**Risk tier: HIGH.** This is patient-facing health information for a vulnerable population
(`docs/good-deed-definition.md`: health domains require credentialed expert sign-off before merge).
Pure toolchain/infra tasks are low–medium; **anything that states a clinical fact, a late effect, a
surveillance recommendation, or anything a survivor could act on is HIGH** and cannot ship without
the dual gate.

**The blocking dual review gate (hard requirement).** Before *any* patient-facing content is
published/handed to a beneficiary:
- **Credentialed clinical sign-off** — a **pediatric/AYA oncologist or a late-effects/survivorship
  specialist** signs off on clinical accuracy, faithfulness to the cited guidelines, and absence of
  harm (no advice creep, correct red-flag/seek-care framing). **No clinician, no ship.**
- **Patient-advocate / survivor sign-off** — a survivor or patient advocate signs off on tone,
  readability, dignity, and **harm-avoidance** (content does not induce fear, fatalism,
  over-screening, or discourage recommended care). **No advocate, no ship.**
- **Both are required and version-scoped.** Neither alone is sufficient; the maintainer **cannot**
  override a "do not ship" from either reviewer on substance. A reviewer "do not ship" blocks
  publication; disagreement is logged and escalated to Hee-Lee Oss governance / a second credentialed
  reviewer.

**Other required reviews.**
- **Maintainer** review on all PRs (toolchain quality, agent-neutral core, gates passing, no
  secrets/PII).
- **Automated gates in CI** (all must pass before review is even requested): citation-coverage,
  mandatory-label, source-similarity (no verbatim copyrighted text), open-access-only source
  allowlist, readability, accessibility, staleness, and faithfulness eval threshold.

**Every page is labeled "Informational, not medical advice — consult your care team"** and routes the
reader to their care team / survivorship clinic for anything individual.

**Definition of Shipped (project):** reviewed, **dual-signed-off** content reaches real
survivors/families through a vetted partner and demonstrably helps them understand or prepare for
their survivorship care, with clinical accuracy and harm-avoidance verified, every assertion sourced,
copyright firewall upheld (no protected expression reproduced), cancer data guardrails honored, and
the no-PII/no-advice stance in force.

---

## Roadmap & milestones

Phased: safety/provenance/licensing first; one exemplar end-to-end through the full gate; then
content; patient-facing content only behind the dual review gate; distribution last and gated on a
secured partner.

- **M0 — Guardrails, schema & cold-start.**
  *Goal:* the safety/provenance/licensing subsystem and an agent-neutral toolchain exist before any
  content.
  *Exit:* late-effect content schema + provenance model merged; the no-medical-advice labeling, the
  source allowlist (open-access/aggregate/de-identified only; controlled-access rejected), and the
  fact-vs-expression copyright policy written; CI gates implemented (citation-coverage, label,
  source-similarity, allowlist, readability, accessibility, staleness) and green on fixtures;
  pnpm/TS/ESM skeleton; review-gate spec written. **Clinical + advocate reviewer recruitment
  started** (dated outreach) so M2 builds against real reviewers.

- **M1 — Provenance pipeline + one exemplar vertical slice.**
  *Goal:* prove the whole pipeline end-to-end on a single high-burden late effect.
  *Exit:* source vetting + provenance recorded for the exemplar's sources (licenses verified); **one**
  late-effect entry (proposal: **anthracycline cardiotoxicity + cardiac surveillance**) drafted,
  fully sourced, passing all automated gates and the faithfulness eval — held as an **internal,
  watermarked exemplar** for reviewer recruitment (not published; the dual gate is not yet staffable).
  **Kill-gate:** if the pipeline cannot produce a faithful, fully-sourced, gate-passing exemplar
  without reproducing protected expression, stop and fix the approach before any content scale-up.

- **M2 — Core late-effects content (dual-gated).**
  *Goal:* the core, high-burden Ewing late effects, each behind the blocking dual review gate.
  *Exit:* entries for cardiac, second-malignancy, fertility/gonadotoxicity, renal (ifosfamide),
  ototoxicity, neuropathy, orthopedic/growth, and neurocognitive/psychosocial — each fully sourced,
  passing automated gates, and **signed off by both an oncologist and an advocate**. *(Gated on
  secured clinical + advocate reviewers — TO BE SECURED.)*

- **M3 — Pediatric→AYA transition module + plain-language/a11y pass.**
  *Goal:* the transition-focused material and a full readability/accessibility sweep.
  *Exit:* survivorship-care-plan explainer, treatment-exposure-summary explainer, pediatric→adult
  transition guidance, and "questions to ask your care team" sets — dual-signed-off; core pages meet
  grade 6–8 readability and WCAG 2.2 AA; health-system-neutrality framing applied (schedules differ
  by guideline/country).

- **M4 — QA, faithfulness eval & publication readiness.**
  *Goal:* prove accuracy/faithfulness and harden for real survivors.
  *Exit:* faithfulness eval across the set meets threshold with expert spot-check; full a11y +
  readability audits pass; staleness fail-safe verified against a simulated guideline update;
  distribution runbook ready; all published-candidate content has recorded dual sign-off.

- **M5 — Distribution & handoff (the deed).**
  *Goal:* reviewed content reaches real survivors/families through a vetted partner.
  *Exit (Definition of Shipped):* a secured partner distributes the library to its survivor
  community; ≥ 1 attested outcome of a survivor/caregiver using it to understand or prepare for
  survivorship care; both sign-offs and guardrails verified; outcomes recorded (de-identified).
  *(Gated on a secured partner — TO BE SECURED.)*

- **M6 — Sustain & guideline-update cadence (post-delivery).**
  *Goal:* durable maintenance with guideline-driven re-review.
  *Exit:* maintenance rotation + ops runbook; a **guideline-update review cadence** wired to the
  staleness fail-safe (new guideline version → auto-flag dependent assertions → re-verify →
  re-dual-sign-off); outcome tracking; a gated process for adding new late-effect topics or
  translations.

Dependencies flow M0 → M1 → M2 → M3 → M4 → M5 → M6. **Reviewer security gates M2–M5** (no dual
reviewers, no patient-facing content). M5 blocks on a secured distribution partner.

---

## Work breakdown

The itemized, schema-mapped backlog lives in **`TASKS.md`**: ~18 tasks across milestones M0–M6 plus
a future backlog, each mapped to the Hee-Lee Oss Task JSON schema, with per-task acceptance criteria for
the most important items, milestone Definitions of Done, and a complete, schema-valid example Task
JSON for the first M0 task (the content schema + provenance/guardrail spec). The first build items
are the **content/provenance schema and the safety/licensing policy** — reflecting their status as
hard product requirements — followed by a **single exemplar vertical slice** (M1) before any content
scale-up, and patient-facing content (M2+) gated on the **dual oncologist + advocate review**.

---

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the schema, the agent-neutral toolchain, CI gates, and merge
  quality. **Cannot** override a clinical or advocate "do not ship."
- **Reviewers / rotation:** at least one engineering reviewer plus the two HIGH-tier reviewers below.
- **Credentialed clinical reviewer (HIGH tier): TO BE SECURED** — a pediatric/AYA oncologist or
  late-effects/survivorship specialist; signs off clinical accuracy + faithfulness + harm-avoidance
  on every patient-facing page before it ships.
- **Patient-advocate / survivor reviewer (HIGH tier): TO BE SECURED** — a survivor or advocate;
  signs off tone, readability, dignity, and harm-avoidance. A **distinct lens** from clinical
  accuracy; both are mandatory.
- **Independence / COI:** reviewers disclose material conflicts (e.g., affiliation with a product or
  trial referenced); sign-off is **version-scoped** (attaches to a specific content version + source
  set; edits require re-sign-off, dovetailing with the staleness model). **Name-use limits:** a
  reviewer's name/credentials may be published only for versions they approved, with consent, and
  may not imply endorsement of the whole library or NCI/COG/ESMO/CCLG endorsement.
- **Disagreement fallback:** either reviewer holds a **veto** on shipping unsafe/inaccurate content;
  a maintainer cannot override on substance. Disagreement is logged and escalated to Hee-Lee Oss governance
  / a second credentialed reviewer; contested content does not ship.
- **Steward (last-mile owner): TO BE SECURED** — owns the partner relationship and the distribution
  that constitutes shipping.
- **Partner / requestor: TO BE SECURED** — a survivorship clinic, sarcoma/AYA advocacy organization,
  or oncology program.
- **Community / board:** license edge cases and any permission requests (e.g., to reproduce a
  specific table) go through Hee-Lee Oss governance.

---

## Dependencies & integrations

- **Source bodies (content inputs):** NCI/PDQ, COG Long-Term Follow-Up Guidelines, IGHG harmonized
  recommendations, ESMO and CCLG guidance, and open-access/aggregate published statistics — each with
  **verified reuse terms** and recorded provenance.
- **External services:** Anthropic Claude API (drafting assistance + faithfulness eval, behind the
  neutral LLM client, per the Claude API skill); static-site hosting for the open library.
- **Hee-Lee Oss pieces:** `packages/schema` (Task JSON), `CLAUDE.md` (work rules + refusal guardrails),
  `docs/good-deed-definition.md` (risk tiers), Hee-Lee Oss governance (license/permission edge cases).
- **Human/decision dependencies (critical path):** a secured **credentialed clinical reviewer** and a
  secured **patient-advocate reviewer** (both block M2+ patient-facing content); a secured
  **distribution partner/steward** (blocks M5). These are the project's true bottlenecks.

---

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| Content read as medical advice; a survivor acts on it instead of consulting their team | High | Critical | "Informational, not medical advice — consult your care team" on every page (build-tested); no individualized/risk content (out of scope, enforced); explicit "seek care / ask your team" routing; advocate harm-avoidance sign-off | Clinical + advocate reviewers |
| Clinical inaccuracy or guideline drift in plain-language synthesis | High | Critical | No-source-no-claim provenance; faithfulness eval (LLM-judge + expert spot-check); **blocking oncologist sign-off**; staleness fail-safe on guideline versions | Clinical reviewer |
| Copyright violation — reproducing COG/ESMO/CCLG/IGHG protected text/tables/figures | Medium | High | Fact-vs-expression firewall; source-similarity check in CI; reviewer confirmation; seek+record explicit permission for any specific table/figure | Maintainer + Clinical reviewer |
| Use of controlled-access or identifiable patient data | Low | Critical | Open-access/aggregate/de-identified **source allowlist**; provenance audit rejecting dbGaP/EGA/individual-level sources; no PII collected by design | Maintainer |
| Content induces fear/fatalism or over-screening | Medium | High | Advocate/survivor harm-avoidance review as a distinct blocking lens; balanced framing; health-system-neutrality | Advocate reviewer |
| No clinical + advocate reviewers secured → patient content blocked | Medium | High | Dated reviewer recruitment (by 2026-10-31); **hold at M1** with only a watermarked internal exemplar; never ship HIGH content unreviewed | Maintainer / Steward |
| No distribution partner secured → cannot reach beneficiaries | Medium | High | Dated outreach (partner by 2026-12-31); **build-vs-mothball/pivot rule** at ~2027-03-31 (pivot to a trusted publisher or mothball — never publish to no vetted channel) | Steward |
| Guideline updated; content silently goes stale | Medium | High | `sourceVersion`/`validUntil` staleness fail-safe auto-flags/withholds + requires re-dual-sign-off; guideline-update review cadence (M6) | Maintainer / Clinical reviewer |
| Survivor cannot apply general content without their own exposure history | High | Medium | Exposure-keyed framing ("applies only if you received…"); survivorship-care-plan + exposure-summary explainers; route to care team for their record | Clinical + advocate reviewers |
| Implying one country's surveillance schedule is universal | Medium | Medium | Health-system-neutrality: state where COG/ESMO/CCLG/IGHG schedules differ; cite each | Clinical reviewer |
| AI hallucination of a fact or citation | Medium | High | Retrieval-grounded drafting; no-source-no-claim; faithfulness eval; human sign-off; source-similarity check | Maintainer |

---

## Security & privacy

**Threat surface.** Inaccurate or harmful health information reaching a vulnerable reader (the
primary harm); copyright infringement of source guidelines; accidental use of
controlled-access/identifiable data; misframing that induces fear or discourages care; supply-chain/
secret leakage in the toolchain.

**Data-minimization by construction.** The library **collects no patient data** — no accounts, no
health intake, no individual risk inputs, nothing to breach or re-identify. Optional feedback is
**anonymous** (free-text discouraged from containing PII; no identifiers, no profiling analytics).
This removes most of the classic privacy attack surface by design.

**Controls.** The safety/provenance/licensing gates are the top control, run in CI and as blocking
human review: citation-coverage, mandatory-label, source-similarity, **open-access-only source
allowlist**, readability, accessibility, staleness, faithfulness eval, and the **dual oncologist +
advocate sign-off**. AI drafting is server-side/tooling-side and grounded; the no-source-no-claim
rule and human review backstop hallucination. **No secrets, tokens, or PII in logs, receipts, or
committed files** (Hee-Lee Oss rule). Dependency and secret scanning in CI. Provenance records may not
point at controlled-access or individual-level sources (audited).

**Abuse/misuse prevention.** The out-of-scope set (individualized advice, diagnosis, prognosis,
dosing, risk scores, controlled-access data, verbatim copyrighted reproduction) is enforced through
schema constraints, CI gates, and the dual review gate — not merely documented. The library is static
education with no interactive clinical tool to misuse.

---

## Sustainability & maintenance

After delivery, a named **maintenance rotation** owns the toolchain and content; the **steward** owns
the partner relationship and outcome tracking. Survivorship guidance **changes** (guidelines are
revised), so a **guideline-update review cadence** is mandatory and **enforced at runtime, not just on
a calendar**: each source's `version`/`validUntil` drives the staleness fail-safe, so when a body
publishes a new guideline version the dependent assertions are **auto-flagged or withheld** until
re-verified against the new version **and re-signed-off by both reviewers**. Outcomes (reach via
partner, attested "better-conversation" instances, anonymous usefulness feedback) are tracked — **not**
engagement metrics. Adding new late-effect topics or translations follows a documented, dual-gated
process and only after the core set is stable; translations are gated per-language by a qualified
reviewer.

---

## Open questions

- **Which late effects make the M2 core set, and in what order?** Proposal: lead with anthracycline
  cardiotoxicity (high burden, clear surveillance) as the M1 exemplar; sequence the rest by burden +
  clarity of guideline consensus. Needs clinical-reviewer input.
- **Which guideline is the "spine" where schedules differ?** COG LTFU (US) vs IGHG harmonized vs
  ESMO/CCLG (EU/UK) recommend on different cadences. Default: present the **harmonized/consensus**
  view (IGHG where available) and **note divergences**, rather than picking one system. Confirm with
  reviewers.
- **Permission for specific tables/figures?** If a particular surveillance table would materially help
  survivors, do we seek written permission from the body (COG/ESMO/CCLG) rather than synthesizing?
  Governance decision per request.
- **Reviewer compensation/credit model** — volunteer vs a future funded lane for review hours (hard
  budget cap) without compromising independence?
- **Distribution channel** — partner-hosted, Hee-Lee Oss-hosted open library, or contributed to an existing
  trusted patient-education publisher? Decided with the secured partner.
- **AYA voice vs caregiver voice** — one entry with dual framings, or separate survivor/caregiver
  variants? Advocate-led decision.
- **Scope of "questions to ask"** sets — keep tightly education-only and avoid anything that reads as
  a self-assessment checklist.

---

## References

- Proposal: `governance/proposals/ewing-survivorship-late-effects.md` (TO BE WRITTEN)
- Portfolio entry: `planning/ROADMAP.md` (Track 8a — `ewing-survivorship-late-effects`) and the
  Track 8 cancer-domain guardrails
- Hee-Lee Oss work rules & refusal guardrails: `CLAUDE.md`
- Good-deed definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- House-style sibling plan: `planning/projects/public-official-guide/{PLAN,TASKS}.md`
- Source bodies (to be license-verified per source): NCI PDQ; Children's Oncology Group Long-Term
  Follow-Up Guidelines for Survivors of Childhood, Adolescent, and Young Adult Cancers; International
  Guideline Harmonization Group (IGHG); ESMO Clinical Practice Guidelines; CCLG

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified and **applied** in this plan (and the
companion `TASKS.md`), beyond a baseline spec:

1. **Dual blocking review gate** — clinical (oncologist) *and* patient-advocate sign-off, both
   required, neither alone sufficient, maintainer cannot override on substance (Exec summary; Quality
   gates; Governance).
2. **Per-assertion provenance schema** with `{ body, document, section, version, retrievedAt,
   evidenceLevel, url, licenseStatus }` (Architecture; Data/licensing).
3. **Fact-vs-expression copyright firewall** — synthesize facts, never reproduce protected guideline
   text/tables/figures; CI source-similarity check (Data/licensing; Risks).
4. **Staleness fail-safe tied to guideline version** — `validUntil` auto-flags/withholds + requires
   re-dual-sign-off when a guideline updates (Data/licensing; Sustainability).
5. **No-medical-advice labeling enforced as a build-time test** on every page, not a footer
   afterthought (Quality gates; Success metrics).
6. **Plain-language reading-level target (grade 6–8)**, measured and gated, with advocate pass
   (Success metrics; M3).
7. **Accessibility WCAG 2.2 AA + translation-ready structure** (Scope; M3/M4).
8. **Exposure-keyed content model** — late effects keyed to specific treatment exposures with
   "applies only if you received…" framing (Architecture; Scope).
9. **No personalized risk score / calculator** — explicit non-goal to avoid advice creep (Goals;
   Scope).
10. **Red-flag "seek care now" routing** where a symptom could be urgent, instead of self-management
    (Architecture; Scope).
11. **Citation-coverage CI gate (no-source-no-claim)** — unsourced clinical claim fails the build
    (Data/licensing; Quality gates).
12. **Reviewer COI / independence / version-scoped sign-off / name-use limits** (Governance).
13. **Open-access-only source allowlist** that rejects controlled-access (dbGaP/EGA) and
    individual-level/identifiable sources in CI (Data/licensing; Security).
14. **Pediatric→AYA transition module** explicitly scoped (survivorship care plan, exposure summary,
    transition to adult care) (Scope; M3).
15. **Dual-audience framing** (survivor-facing + caregiver-facing; AYA voice) (Architecture; Scope).
16. **Separate lived-experience review lens** from clinical-accuracy review — two distinct mandatory
    reviewers (Governance; Quality gates).
17. **Harm-avoidance review** — content must not induce fear/fatalism/over-screening or discourage
    recommended care (Quality gates; Risks).
18. **Translation-ready/i18n content model** now, with per-language reviewer gating deferred to
    backlog (Architecture; Sustainability).
19. **Content versioning + change log** so every published change is traceable to a reviewed version
    (Governance; Sustainability).
20. **Dated partner/reviewer acquisition plan + build-vs-mothball/pivot decision rule** — never
    publish HIGH-risk health content to no reviewer/no beneficiary (Exec summary; Risks; M5).
21. **One vertical-slice exemplar end-to-end through the full gate before scaling content** (M1
    kill-gate).
22. **Faithfulness eval** (LLM-judge + expert spot-check) that each plain-language assertion is
    faithful to its cited source (Architecture; Success metrics; M4).
23. **Zero PII / no-data-collection by construction** — no accounts/health intake; anonymous,
    non-profiling feedback (Data/licensing; Security).
24. **Explicit out-of-scope list** (no diagnosis/prognosis/dosing/individual risk/trial-matching)
    enforced by schema + gates + review (Scope; Security).
25. **Geographic/health-system neutrality** — surveillance schedules differ by guideline/country;
    present harmonized/consensus view and note divergences (Scope; Open questions; Risks).

---

## Review sign-off

**Reviewer:** plan author (senior staff engineer + TPM), self-review pass · 2026-06-28.

**Completeness check.** All 17 required PLAN sections present and in spec order; `TASKS.md` companion
present with schema mapping, milestone tables, per-task acceptance criteria, milestone DoDs, backlog,
and a schema-valid example Task JSON. *Data, licensing & compliance* and *Quality, review & risk
gates* both **lead with the binding cancer guardrails**, and the oncologist + patient-advocate review
is an explicit **blocking** gate before any deed ships (HIGH tier). Appendix A lists 25 applied
improvements.

**Correctness check & fixes applied during review.**
- Verified Task JSON example against `packages/schema/src/schemas.ts`: all `required` fields present;
  enums valid (`type=design-spec`, `lane=donated`, `priority=high`, `riskTier=high`,
  `deliverable=document`, `tokenEstimate=medium`, `status=open`); `verifiedNeed:false`;
  `acceptanceCriteria` non-empty; `output` non-empty; no extra properties (`additionalProperties:
  false`). Donated lane → `fundedBudgetUsd` correctly omitted.
- Confirmed `riskTier: high` on all patient-facing tasks (M2/M3 content, M5 handoff); toolchain/infra
  tasks set to low/medium per the definition.
- Confirmed `verifiedNeed: false` across the backlog (no partner/reviewer secured) and `requestor: TO
  BE SECURED` where applicable.
- Confirmed the licensing nuance is conservative: NCI/PDQ public-domain (with trademark/no-endorsement
  caveat); COG/ESMO/CCLG/IGHG cited-not-reproduced via the fact-vs-expression firewall; output
  CC-BY-4.0 (our synthesis) / MIT (code).
- Confirmed the cancer guardrail (open-access/aggregate/de-identified only; controlled-access +
  identifiable data out of scope) is enforced as a CI source-allowlist gate, not just prose.

**Outstanding items needing a human decision (surfaced, not resolved):** secure the credentialed
clinical reviewer and patient-advocate reviewer (gates M2); secure a distribution partner/steward
(gates M5); choose the guideline "spine" (IGHG-harmonized vs system-specific); decide whether to seek
permission for any specific source table/figure; reviewer compensation/credit model. These are
tracked in *Open questions* and the dated acquisition plan.

**Sign-off status:** Draft approved for circulation to a maintainer and prospective HIGH-tier
reviewers. **Not** approved for any content publication — that requires the dual oncologist +
advocate gate, which is `TO BE SECURED`.
