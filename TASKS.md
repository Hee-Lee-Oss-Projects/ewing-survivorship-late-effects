# Ewing-Survivorship-Late-Effects — TASKS.md

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Backlog for **Ewing-Survivorship-Late-Effects** (slug: `ewing-survivorship-late-effects`), an open,
plain-language, **education-only** survivorship/late-effects resource library for Ewing sarcoma
survivors across the **pediatric → AYA** transition, synthesized from vetted bodies (NCI/PDQ, COG
LTFU, IGHG, ESMO, CCLG). See `PLAN.md` for full context.

**Binding guardrails (lead everything):**
- **Cancer data guardrail:** only **open-access / aggregate / de-identified** sources;
  **controlled-access (dbGaP/EGA) and any identifiable patient data are OUT OF SCOPE**; verify each
  source's license before its content ships.
- **No medical advice:** patient-facing content is education only, sourced, labeled *"Informational,
  not medical advice — consult your care team."*
- **HIGH risk tier, blocking dual review gate:** **no patient-facing page ships without sign-off from
  BOTH a credentialed pediatric/AYA oncologist AND a patient advocate.** Neither alone suffices.
- **Provenance on every assertion** (no-source-no-claim). **Fact-vs-expression copyright firewall**
  (synthesize + cite; never reproduce protected guideline text/tables/figures).

No partner, clinical reviewer, advocate reviewer, or steward is yet secured, so delivery-dependent
tasks carry `requestor: TO BE SECURED` and `verifiedNeed: false`.

## How these tasks map to Hee-Lee Oss

Each task becomes a Hee-Lee Oss **Task JSON** validated against `packages/schema/src/schemas.ts`. Field
mapping:

- **id** — stable slug `ewing-survivorship-late-effects-<area>-NNN`.
- **title** — the task title in the milestone table.
- **project** — `ewing-survivorship-late-effects`.
- **type** — one of `code | research | writing | data | design-spec | maintenance`.
- **lane** — `donated` (default; no funded tasks planned. Any `funded` task must add
  `fundedBudgetUsd` with a hard cap).
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["health","oncology","survivorship","patient-education","ewing-sarcoma"]`.
- **riskTier** — `low | medium | high`. **Any patient-facing clinical content is `high`**; provenance/
  guardrail policy is `high`; toolchain/infra is `low`–`medium`.
- **urgent** — boolean (no urgent tasks at cold-start).
- **deliverable** — `pr | dataset | document | translation`.
- **tokenEstimate** — `small | medium | large` (maps to the Size column).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — partner/steward/reviewer; `TO BE SECURED` where unknown.
- **verifiedNeed** — `true` only once a specific partner/need is confirmed; **currently `false`
  everywhere** (no partner secured).
- **outputLicense** — content/docs: `CC-BY-4.0`; toolchain code: `MIT`.

Size legend: small ≈ `small`, med ≈ `medium`, large ≈ `large`.
Reviewer "Oncologist (HIGH)" = credentialed pediatric/AYA oncologist or late-effects specialist
(**TO BE SECURED**). "Advocate (HIGH)" = patient-advocate/survivor reviewer (**TO BE SECURED**).
Patient-facing content requires **both**.

---

## Milestone M0 — Guardrails, schema & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-schema-001 | Content + provenance schema and safety/licensing policy spec (cancer guardrails, no-advice, dual-review, fact-vs-expression) | design-spec | medium | high | document | — | Maintainer + Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-repo-002 | pnpm + TS/ESM monorepo + static-site + CI skeleton | code | small | low | pr | — | Maintainer |
| ewing-survivorship-late-effects-gates-003 | CI gates: citation-coverage, no-advice-label, source-similarity, open-access source allowlist | code | medium | high | pr | 001, 002 | Maintainer + Oncologist (HIGH) |
| ewing-survivorship-late-effects-gates-004 | CI gates: readability, accessibility (WCAG 2.2 AA), staleness fail-safe (validUntil) | code | medium | medium | pr | 001, 002 | Maintainer |
| ewing-survivorship-late-effects-recruit-005 | Reviewer + partner recruitment plan (dated; oncologist + advocate + distribution partner) | research | small | medium | document | 001 | Maintainer + Steward |

**Acceptance criteria — key tasks**

- **ewing-survivorship-late-effects-schema-001** (schema + safety/licensing policy)
  - Defines the Late-Effect Entry schema: `exposures[]`, `sections[]`, `assertions[]` each with
    `sourceRef`, `provenance[]` (`body, document, section, version, retrievedAt, evidenceLevel?, url,
    licenseStatus`), mandatory `labels` (no-advice), `validUntil`, and `review` (clinical + advocate
    sign-off, version-scoped).
  - States the **cancer data guardrail** (open-access/aggregate/de-identified only; controlled-access
    dbGaP/EGA and identifiable data OUT OF SCOPE) and the **open-access source allowlist** the gates
    enforce.
  - States the **fact-vs-expression copyright firewall** (synthesize + cite; never reproduce
    protected guideline text/tables/figures) and per-body license posture (NCI/PDQ public-domain w/
    trademark caveat; COG/ESMO/CCLG/IGHG cited-not-reproduced).
  - Mandates the **"Informational, not medical advice — consult your care team"** label on every page
    and the **blocking dual review gate** (oncologist + advocate, both required) as Definition of
    Shipped.
  - Enumerates out-of-scope content (diagnosis, prognosis, dosing, individual risk score,
    trial-matching) and the no-PII/no-data-collection stance.
  - Reviewed/signed by a credentialed oncologist + an advocate (recorded in the reviewers ledger).

- **ewing-survivorship-late-effects-gates-003** (safety/licensing CI gates)
  - **Citation-coverage:** any clinical assertion without a resolvable `sourceRef` **fails the build**.
  - **No-advice-label:** every published page carries the mandatory label; missing label fails.
  - **Source-similarity:** flags passages too close to source text (copyright firewall); over
    threshold fails and routes to review.
  - **Open-access source allowlist:** a provenance record pointing at a controlled-access
    (dbGaP/EGA), individual-level, or identifiable source **fails the build**.

- **ewing-survivorship-late-effects-recruit-005** (dated recruitment plan)
  - Names target reviewer profiles (pediatric/AYA oncologist or late-effects specialist; survivor/
    advocate) and partner profiles (survivorship clinic, sarcoma/AYA advocacy org).
  - Fixes the dated plan: reviewers + ≥ 2 partners engaged by 2026-08-31; ≥ 1 oncologist + 1 advocate
    secured by 2026-10-31 (gates M2); distribution partner by 2026-12-31 (gates M5); build-vs-mothball/
    pivot decision by ~2027-03-31.
  - Records that all delivery-dependent tasks stay `verifiedNeed:false` / `TO BE SECURED` until
    secured.

**M0 Definition of Done:** content + provenance schema and the safety/licensing policy
(cancer-guardrail-led, expert-reviewed) merged; pnpm/TS/ESM + static-site + CI skeleton green; the
safety/licensing and quality CI gates implemented and passing on fixtures; dated reviewer/partner
recruitment plan recorded. **No patient-facing content yet.**

---

## Milestone M1 — Provenance pipeline + one exemplar vertical slice

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-sources-006 | Source vetting + provenance for the exemplar (verify reuse terms; record license status) | data | medium | high | dataset | 001, 003 | Oncologist (HIGH) + Maintainer |
| ewing-survivorship-late-effects-exemplar-007 | Exemplar entry: anthracycline cardiotoxicity + cardiac surveillance (internal, watermarked) | writing | medium | high | document | 003, 004, 006 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-eval-008 | Faithfulness eval harness (LLM-judge + expert spot-check) on the exemplar | code | small | medium | pr | 007 | Maintainer |

**Acceptance criteria — key tasks**

- **ewing-survivorship-late-effects-sources-006** (source vetting)
  - Reuse terms **verified and recorded per source** (NCI/PDQ public-domain; COG/ESMO/CCLG/IGHG
    cited-not-reproduced); only open-access/aggregate/de-identified sources enabled.
  - Provenance recorded (`body, document, section, version, retrievedAt, evidenceLevel?, url,
    licenseStatus`); any controlled-access/identifiable source is **rejected** by the allowlist.

- **ewing-survivorship-late-effects-exemplar-007** (vertical-slice exemplar)
  - One late-effect entry drafted end-to-end, **fully sourced** (every assertion has a `sourceRef`),
    passing **all** automated gates and the faithfulness eval; exposure-keyed ("applies if you
    received an anthracycline"); no-advice label present; red-flag/seek-care framing correct.
  - **Held internal + watermarked, NOT published** (dual reviewers not yet secured); usable for
    reviewer recruitment.
  - **Kill-gate:** if a faithful, fully-sourced, gate-passing exemplar cannot be produced without
    reproducing protected expression, **stop and fix the pipeline** before M2.

**M1 Definition of Done:** source vetting + provenance recorded for the exemplar (licenses verified);
the anthracycline-cardiotoxicity exemplar drafted, fully sourced, passing all automated gates + the
faithfulness eval, held as an internal watermarked artifact; pipeline kill-gate satisfied. **Still
not published** — patient publication requires the dual gate (M2+).

---

## Milestone M2 — Core late-effects content (dual-gated)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-cardiac-009 | Cardiac late effects (anthracycline) entry — publish-ready, dual-signed | writing | medium | high | document | 007 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-secondca-010 | Second malignant neoplasms (alkylator/radiation) entry | writing | medium | high | document | 006, 009 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-fertility-011 | Gonadotoxicity / fertility entry | writing | medium | high | document | 006, 009 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-renal-012 | Ifosfamide nephrotoxicity / renal surveillance entry | writing | medium | high | document | 006, 009 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-msk-013 | Orthopedic / musculoskeletal / growth (surgery + radiation) entry | writing | medium | high | document | 006, 009 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-neuro-014 | Ototoxicity, vincristine neuropathy, neurocognitive/psychosocial entries | writing | large | high | document | 006, 009 | Oncologist (HIGH) + Advocate (HIGH) |

**Acceptance criteria — key tasks**

- **ewing-survivorship-late-effects-cardiac-009** (cardiac entry, publish-ready)
  - Promotes the M1 exemplar to publish-ready; every assertion sourced; exposure-keyed; no-advice
    label; correct red-flag/seek-care routing; reading grade 6–8; WCAG 2.2 AA.
  - Passes all automated gates **and** carries **both** version-scoped sign-offs (oncologist +
    advocate). **Neither sign-off alone permits publish.**

- **ewing-survivorship-late-effects-fertility-011** (fertility entry)
  - Plain-language, education-only; keyed to alkylator exposure; covers awareness of
    fertility-preservation as a topic to raise with the care team — **no individualized advice or
    risk figure**.
  - Health-system-neutral where guidance differs; fully sourced; dual-signed.

- **ewing-survivorship-late-effects-neuro-014** (oto/neuro/psychosocial bundle)
  - Each sub-entry fully sourced and exposure-keyed; psychosocial/AYA mental-health framing reviewed
    by the **advocate** for harm-avoidance (no fear/fatalism); seek-care routing for urgent symptoms.
  - Dual-signed; passes all gates.

**M2 Definition of Done:** the core high-burden Ewing late-effect entries (cardiac, second
malignancy, fertility, renal, orthopedic/growth, oto/neuro/psychosocial) are fully sourced, pass all
automated gates, and each carries **both** oncologist and advocate version-scoped sign-offs.
*(Gated on secured dual reviewers — TO BE SECURED; until then, content is drafted/held, not
published.)*

---

## Milestone M3 — Pediatric→AYA transition module + plain-language/a11y pass

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-transition-015 | Pediatric→AYA transition module (survivorship care plan, exposure summary, transition to adult care) | writing | medium | high | document | 009 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-questions-016 | "Questions to ask your care team" sets (per late effect + transition) | writing | small | high | document | 015 | Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-a11y-017 | Plain-language (grade 6–8) + WCAG 2.2 AA + health-system-neutrality sweep across the set | maintenance | medium | medium | pr | 014, 015, 016 | Maintainer + Advocate (HIGH) |

**Acceptance criteria — key tasks**

- **ewing-survivorship-late-effects-transition-015** (transition module)
  - Explains what a survivorship care plan and a treatment-exposure summary are and why they matter
    at the pediatric→adult handoff; education-only; routes to the care team/survivorship clinic.
  - Fully sourced; dual-signed; AYA-appropriate voice; caregiver framing included.

- **ewing-survivorship-late-effects-questions-016** (questions sets)
  - Education-only prompt lists tied to each late effect + the transition; **not** a self-assessment
    or triage checklist; advocate-reviewed for tone; sourced where they encode a recommendation.

**M3 Definition of Done:** transition module + question sets dual-signed and published-ready; the full
set meets grade 6–8 readability and WCAG 2.2 AA; health-system-neutrality framing applied (schedules
differ by guideline/country, each cited).

---

## Milestone M4 — QA, faithfulness eval & publication readiness

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-qa-018 | Full faithfulness eval + a11y/readability audit + staleness fail-safe verification + distribution runbook | code | medium | high | pr | 014, 015, 016, 017 | Maintainer + Oncologist (HIGH) + Advocate (HIGH) |

**Acceptance criteria — ewing-survivorship-late-effects-qa-018**
- Faithfulness eval across the whole set meets the agreed threshold **with expert spot-check**; any
  failing assertion is fixed or withheld.
- Full accessibility + readability audits pass; staleness fail-safe verified against a **simulated
  guideline-version update** (dependent assertions auto-flag/withhold + require re-dual-sign-off).
- Distribution runbook written; every publish-candidate page has recorded dual sign-off.

**M4 Definition of Done:** the library is publication-ready — faithfulness, accessibility,
readability, and staleness all verified; dual sign-off recorded across all candidate content;
distribution runbook ready. (Publication still gated on a secured partner — M5.)

---

## Milestone M5 — Distribution & handoff (the deed)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-partner-019 | Secure distribution partner/steward + final guardrail + dual sign-off verification | research | medium | high | document | 018 | Steward + Oncologist (HIGH) + Advocate (HIGH) |
| ewing-survivorship-late-effects-handoff-020 | Distribute to survivors via partner; record attested usefulness outcomes (de-identified) | maintenance | medium | high | document | 019 | Steward + Advocate (HIGH) |

**Acceptance criteria — key tasks**

- **ewing-survivorship-late-effects-partner-019** (secure partner + final verification)
  - A real survivorship clinic / sarcoma-or-AYA advocacy org is secured as distribution partner;
    steward assigned; `verifiedNeed` flips to `true`.
  - Final verification: all published content carries dual sign-off; cancer data guardrails +
    copyright firewall + no-PII stance confirmed.
  - Driven by the **dated plan**; if no partner by **~2027-03-31**, apply the **build-vs-mothball/
    pivot rule** (pivot to a trusted patient-education publisher or mothball to maintenance-only —
    recorded in governance — **never** publish HIGH-risk health content to no vetted channel).

- **ewing-survivorship-late-effects-handoff-020** (closed loop — the deed)
  - Reviewed content reaches real survivors/families through the partner; ≥ 1 attested instance of a
    survivor/caregiver using it to understand or prepare for survivorship care (de-identified,
    anonymous feedback, no PII).
  - No-advice framing upheld; both sign-offs and guardrails verified throughout.

**M5 Definition of Done:** project-level **Definition of Shipped** met — dual-signed-off content
reaches real survivors/families through a vetted partner and demonstrably helps them, with clinical
accuracy + harm-avoidance verified, every assertion sourced, copyright firewall + cancer guardrails +
no-PII stance upheld, outcomes recorded (de-identified). *(Gated on a secured partner — TO BE
SECURED.)*

---

## Milestone M6 — Sustain & guideline-update cadence (post-delivery)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-ops-021 | Ops runbook + guideline-update review cadence + maintenance rotation + outcome tracking | maintenance | medium | medium | document | 020 | Maintainer + Steward + Oncologist (HIGH) |

**Acceptance criteria — ewing-survivorship-late-effects-ops-021**
- Runbook covers deploy, source re-verification, and the **guideline-update cadence** wired to the
  staleness fail-safe (new guideline version → auto-flag dependent assertions → re-verify →
  **re-dual-sign-off**).
- Named maintenance rotation; outcome tracking (reach via partner, attested usefulness — not
  engagement); documented, dual-gated process for adding new late-effect topics or translations.

**M6 Definition of Done:** project sustainably maintained with a guideline-driven re-review cadence, a
rotation owning it, outcomes tracked, and a gated expansion/translation process.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
|---|---|---|---|---|---|---|
| ewing-survivorship-late-effects-i18n-022 | Translations of the library (per-language, reviewer-gated) | translation | large | high | translation | Only after M6; each language gated by a qualified clinical + advocate reviewer |
| ewing-survivorship-late-effects-pulmonary-023 | Pulmonary / other organ-specific late effects (Ewing-relevant exposures) | writing | medium | high | document | Extends the core set; full sourcing + dual sign-off |
| ewing-survivorship-late-effects-permissions-024 | Seek + record permission to reproduce specific high-value source tables/figures | research | small | medium | document | Only if synthesis is insufficient; governance-routed |
| ewing-survivorship-late-effects-print-025 | Printable, low-bandwidth survivor handout pack (CC-BY) | writing | medium | high | document | Derived from dual-signed content; re-check label + a11y |
| ewing-survivorship-late-effects-feedback-026 | Anonymous, no-PII feedback channel + outcome instrumentation | code | small | medium | pr | No profiling analytics; anonymous only |

---

## Acceptance criteria — rows previously without an explicit block

The milestone tables above named several rows without spelling out their acceptance criteria inline.
Those criteria are now authored in the machine-readable `tasks/*.json` files and are summarized here
so `TASKS.md` stays consistent with the JSON set:

- **ewing-survivorship-late-effects-repo-002** — pnpm/TS/ESM workspace builds clean
  (`pnpm build && pnpm test && pnpm lint`); static-site package scaffolded (no content yet); CI green
  on an empty fixture with hooks for the 003/004 gates; no PII, no third-party analytics, no
  agent/vendor-specific logic in core.
- **ewing-survivorship-late-effects-gates-004** — readability gate flags pages outside grade 6–8;
  accessibility gate fails on WCAG 2.2 AA violations; staleness fail-safe auto-flags/withholds any
  assertion past its guideline-version `validUntil` until re-verified and re-dual-signed-off; all
  exercised by passing/failing fixtures.
- **ewing-survivorship-late-effects-eval-008** — per-assertion faithfulness score vs cited source;
  automated LLM-judge + structured expert spot-check; sub-threshold assertions surfaced for
  fix-or-withhold; provider-neutral; no PII/source full-text in logs.
- **secondca-010 / renal-012 / msk-013 / pulmonary-023** — plain-language, education-only entries
  keyed to the relevant exposure(s); every assertion sourced; no-advice label; correct
  red-flag/seek-care routing; grade 6–8; WCAG 2.2 AA; no diagnosis/prognosis/dosing/individual risk
  figure; health-system-neutral where guidance differs; pass all gates **and** carry both
  oncologist + advocate version-scoped sign-offs.
- **ewing-survivorship-late-effects-a11y-017** — every entry measured at grade 6–8 (advocate-confirmed);
  every page passes WCAG 2.2 AA; health-system-neutrality framing applied and cited; no substantive
  clinical change without re-entering dual review.
- **ewing-survivorship-late-effects-permissions-024** — undertaken only where synthesis is
  demonstrably insufficient; governance-routed decision recorded; permission requests/outcomes and
  granted terms recorded per source; any reproduced element carries recorded permission + attribution.
- **ewing-survivorship-late-effects-print-025** — derived only from already dual-signed content;
  every assertion retains its `sourceRef`; no-advice label present in print; print a11y/readability
  re-checked (grade 6–8); any substantive change re-enters dual review; CC-BY-4.0.
- **ewing-survivorship-late-effects-feedback-026** — anonymous, no PII, no accounts, no health
  intake; no profiling analytics (attested usefulness + reach, not engagement); no identifiable data
  stored/logged; privacy stance verified in tests.

## Fan-out note

This decomposition maps **one Task JSON per backlog row** — no fabricated fan-out. The two
dimensions that *could* expand (translations `i18n-022`; pulmonary/other organ entries `pulmonary-023`)
are **open-ended / not enumerated** in `PLAN.md`, and the dual-reviewer + distribution partner remain
**TO BE SECURED**, so each is kept as a single **representative** task. Concrete languages and
additional organ-specific entries are added only on reviewer/partner confirmation — none are invented
here. The `neuro-014` row bundles three exposure-keyed sub-entries (ototoxicity, vincristine
neuropathy, neurocognitive/psychosocial) under its single stable id, per the plan's own id pattern.
All delivery-dependent tasks stay `verifiedNeed: false` / `requestor: TO BE SECURED`, and no
patient-facing entry is authored as advice — entries remain education-only, fully sourced, and gated
on the blocking oncologist + advocate dual sign-off.

## Generated task index

All 26 backlog rows now have a schema-valid `tasks/<id>.json` (validated against the Hee-Lee Oss
taskSchema). Seed `…-schema-001` is unchanged; the rest were generated by this decomposition.

| ID | Type | Risk | Deliverable | File |
|---|---|---|---|---|
| ewing-survivorship-late-effects-schema-001 | design-spec | high | document | `tasks/ewing-survivorship-late-effects-schema-001.json` (seed) |
| ewing-survivorship-late-effects-repo-002 | code | low | pr | `tasks/ewing-survivorship-late-effects-repo-002.json` |
| ewing-survivorship-late-effects-gates-003 | code | high | pr | `tasks/ewing-survivorship-late-effects-gates-003.json` |
| ewing-survivorship-late-effects-gates-004 | code | medium | pr | `tasks/ewing-survivorship-late-effects-gates-004.json` |
| ewing-survivorship-late-effects-recruit-005 | research | medium | document | `tasks/ewing-survivorship-late-effects-recruit-005.json` |
| ewing-survivorship-late-effects-sources-006 | data | high | dataset | `tasks/ewing-survivorship-late-effects-sources-006.json` |
| ewing-survivorship-late-effects-exemplar-007 | writing | high | document | `tasks/ewing-survivorship-late-effects-exemplar-007.json` |
| ewing-survivorship-late-effects-eval-008 | code | medium | pr | `tasks/ewing-survivorship-late-effects-eval-008.json` |
| ewing-survivorship-late-effects-cardiac-009 | writing | high | document | `tasks/ewing-survivorship-late-effects-cardiac-009.json` |
| ewing-survivorship-late-effects-secondca-010 | writing | high | document | `tasks/ewing-survivorship-late-effects-secondca-010.json` |
| ewing-survivorship-late-effects-fertility-011 | writing | high | document | `tasks/ewing-survivorship-late-effects-fertility-011.json` |
| ewing-survivorship-late-effects-renal-012 | writing | high | document | `tasks/ewing-survivorship-late-effects-renal-012.json` |
| ewing-survivorship-late-effects-msk-013 | writing | high | document | `tasks/ewing-survivorship-late-effects-msk-013.json` |
| ewing-survivorship-late-effects-neuro-014 | writing | high | document | `tasks/ewing-survivorship-late-effects-neuro-014.json` |
| ewing-survivorship-late-effects-transition-015 | writing | high | document | `tasks/ewing-survivorship-late-effects-transition-015.json` |
| ewing-survivorship-late-effects-questions-016 | writing | high | document | `tasks/ewing-survivorship-late-effects-questions-016.json` |
| ewing-survivorship-late-effects-a11y-017 | maintenance | medium | pr | `tasks/ewing-survivorship-late-effects-a11y-017.json` |
| ewing-survivorship-late-effects-qa-018 | code | high | pr | `tasks/ewing-survivorship-late-effects-qa-018.json` |
| ewing-survivorship-late-effects-partner-019 | research | high | document | `tasks/ewing-survivorship-late-effects-partner-019.json` |
| ewing-survivorship-late-effects-handoff-020 | maintenance | high | document | `tasks/ewing-survivorship-late-effects-handoff-020.json` |
| ewing-survivorship-late-effects-ops-021 | maintenance | medium | document | `tasks/ewing-survivorship-late-effects-ops-021.json` |
| ewing-survivorship-late-effects-i18n-022 | writing | high | translation | `tasks/ewing-survivorship-late-effects-i18n-022.json` |
| ewing-survivorship-late-effects-pulmonary-023 | writing | high | document | `tasks/ewing-survivorship-late-effects-pulmonary-023.json` |
| ewing-survivorship-late-effects-permissions-024 | research | medium | document | `tasks/ewing-survivorship-late-effects-permissions-024.json` |
| ewing-survivorship-late-effects-print-025 | writing | high | document | `tasks/ewing-survivorship-late-effects-print-025.json` |
| ewing-survivorship-late-effects-feedback-026 | code | medium | pr | `tasks/ewing-survivorship-late-effects-feedback-026.json` |

> Note: `i18n-022` is `type: "writing"` + `deliverable: "translation"` (translation is a deliverable,
> not a task type), licensed source-compatibly (CC-BY-4.0, matching our own content). Toolchain tasks
> (002/003/004/008/017/018/026) are `outputLicense: MIT`; content/datasets/docs are `CC-BY-4.0`.

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task
(`ewing-survivorship-late-effects-schema-001`):

```json
{
  "id": "ewing-survivorship-late-effects-schema-001",
  "title": "Content + provenance schema and safety/licensing policy spec (cancer guardrails, no-advice, dual-review, fact-vs-expression)",
  "project": "ewing-survivorship-late-effects",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["health", "oncology", "survivorship", "patient-education", "ewing-sarcoma"],
  "riskTier": "high",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "medium",
  "status": "open",
  "context": "Ewing-Survivorship-Late-Effects is an open, education-only survivorship/late-effects resource library for Ewing sarcoma survivors across the pediatric-to-AYA transition, synthesizing recommendations from vetted bodies (NCI/PDQ, COG Long-Term Follow-Up Guidelines, IGHG, ESMO, CCLG) into plain language. This is HIGH risk-tier, patient-facing health information for a vulnerable population, so safety, provenance, and licensing lead the architecture. Binding cancer guardrails: only open-access/aggregate/de-identified sources; controlled-access (dbGaP/EGA) and any identifiable patient data are OUT OF SCOPE. No medical advice; every assertion sourced; no page ships without BOTH a credentialed oncologist and a patient-advocate sign-off. This cold-start task specifies the content/provenance schema and the safety/licensing policy that all later content and tooling must implement and be tested against, before any patient-facing content is drafted. No partner, clinical reviewer, or advocate reviewer is yet secured.",
  "objective": "Write the authoritative content + provenance schema and safety/licensing policy: the Late-Effect Entry schema (exposures, sections, per-assertion sourceRefs, provenance fields, mandatory no-advice labels, validUntil staleness, and version-scoped clinical+advocate review), the binding cancer data guardrail and open-access source allowlist, the fact-vs-expression copyright firewall and per-body license posture, the blocking dual-review gate as Definition of Shipped, the explicit out-of-scope set, and the no-PII/no-data-collection stance.",
  "acceptanceCriteria": [
    "Defines the Late-Effect Entry schema with exposures[], sections[], assertions[] each carrying >=1 sourceRef, provenance[] (body, document, section, version, retrievedAt, evidenceLevel?, url, licenseStatus), mandatory no-advice labels, validUntil, and a review object requiring version-scoped clinical AND advocate sign-off",
    "States the binding cancer data guardrail (open-access/aggregate/de-identified ONLY; controlled-access dbGaP/EGA and any identifiable patient data OUT OF SCOPE) and the open-access source allowlist the CI gates enforce",
    "States the fact-vs-expression copyright firewall (synthesize facts and cite; never reproduce protected guideline text/tables/figures) and the per-body license posture (NCI/PDQ public-domain with trademark/no-endorsement caveat; COG/ESMO/CCLG/IGHG cited-not-reproduced)",
    "Mandates the 'Informational, not medical advice - consult your care team' label on every page and the blocking dual review gate (credentialed oncologist + patient advocate, both required, maintainer cannot override on substance) as the Definition of Shipped",
    "Enumerates the explicit out-of-scope set (diagnosis, prognosis, dosing, individualized risk score/calculator, clinical-trial matching) and the no-PII / no-data-collection stance (no accounts, no health intake, anonymous non-profiling feedback)",
    "Defines the no-source-no-claim rule and the validUntil staleness fail-safe (a claim past its guideline version's validUntil is auto-flagged/withheld until re-verified and re-dual-signed-off)",
    "Reviewed and signed off by a credentialed pediatric/AYA oncologist (or late-effects specialist) and a patient-advocate reviewer, recorded in the reviewers ledger"
  ],
  "resources": [
    "planning/projects/ewing-survivorship-late-effects/PLAN.md",
    "planning/ROADMAP.md",
    "CLAUDE.md",
    "docs/good-deed-definition.md",
    "packages/schema/src/schemas.ts"
  ],
  "output": "A reviewed schema + policy specification document defining the Late-Effect Entry content/provenance schema, the binding cancer data guardrails and open-access source allowlist, the fact-vs-expression copyright firewall, the no-medical-advice labeling, the blocking dual oncologist+advocate review gate, the out-of-scope set, and the no-PII stance - the contract that the CI gates (ewing-survivorship-late-effects-gates-003/004) and all content tasks (M1+) implement and are verified against.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
