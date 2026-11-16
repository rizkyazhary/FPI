# FSI Hackathon Brainstorm Register

## Register metadata

| Field | Value |
|---|---|
| Created | 2026-11-16 |
| Last updated | 2026-11-16 |
| Current round | BR-005 — PRD and TRD v0.1 created from the verification BRD |
| Purpose | Preserve all brainstorm ideas, comparisons, assumptions, questions, and decisions in a consistent structure |
| User instruction | "every brainstorm make sure all recorded structured" |
| Decision status | FSI-005 is the current user-proposed discussion focus; no final hackathon selection or implementation scope approved |

## Recording conventions

- Give every idea a permanent ID; preserve rejected or deferred ideas and their reasons.
- Update this register whenever a brainstorm adds, refines, compares, or rules out an idea.
- Use the same fields for each idea: theme, users, problem, proposed MVP, data, demo, value measures, risks, open questions, and status.
- Separate user-confirmed decisions from assistant recommendations and unvalidated assumptions.
- Record revisions in the round log; do not silently replace earlier decisions.
- Business metrics are proposed measurements, not proven benefits or promised outcomes.

## Source and challenge constraints

Source: [User-supplied challenge slide](file:///Users/rizkyazhary/.qoder/tmp/-Users-rizkyazhary-Documents-Cakra-rizky-di-cakra-Qoder-BFSI-Initiatives/images/78defc71-c219-4f1c-a350-3d5ea30bcb70/e91cca46-f53e-4e74-a5ca-7954ab3b4f69.jpeg).

| Area | Requirement from the slide |
|---|---|
| Themes | Customer complaint tracking; payment reconciliation; loan document completeness; insurance claim fraud detection |
| Data | Synthetic CSV/JSON only |
| Logic | Fixed rules; no ML, OCR, or live integrations |
| Lending boundary | Check completeness, not creditworthiness; no credit decision |
| Insurance boundary | Flags are not proof of fraud; a human reviewer confirms or clears flags; no automatic claim rejection |
| Deliverables | Website and mobile app; source code; BRD/PRD/TRD; team presentation; demo outcomes |
| Quality evidence | Functional, performance, and penetration-test scenarios; automated tests; QA report |
| Workflow evidence | Diagnose → build → stress-test; show iteration evidence and actual usage within budget |
| Stated tooling | Slide references Sonus; whether that requirement applies unchanged to this team's submission remains to be confirmed |

## Idea index

| ID | Idea | Theme | Intended operational user | Relative complexity | Status |
|---|---|---|---|---|---|
| FSI-001 | Complaint Rescue | Banking / customer complaints | Customer support and payment operations | Low, consistent with slide theme | Proposed |
| FSI-002 | SettleCheck | Payments and merchant services | Merchant finance or payment operations | Medium, consistent with slide theme | Proposed |
| FSI-003 | LoanReady | Lending and financing | Relationship managers and loan operations | Low, consistent with slide theme | Proposed |
| FSI-004 | ClaimLens | Insurance | Claims reviewers | Medium, consistent with slide theme | Proposed |
| FSI-005 | Multifinance Verification Orchestrator — working title | Lending / customer verification | Multifinance verification team; individual and corporate customers | Full concept exceeds the slide's low–medium scope; narrowed demo not yet agreed | User-proposed; current discussion focus |

FSI-001 through FSI-004 are assistant-proposed workflows, not verified deployments or customer-validated demand. Their data fields, edge cases, and open questions are proposed elaborations, not approved requirements. FSI-005 records the user's operational problem and proposed concept; proposed safeguards and unresolved design choices are identified separately.

## FSI-001 — Complaint Rescue

| Field | Recorded idea |
|---|---|
| Theme | Customer Complaint Tracker |
| Problem | A customer's account is debited but the recipient has not received the transfer; handoffs between support and payment operations can delay resolution |
| Target users | Customer, customer-support agent, payment-operations case owner |
| Proposed MVP | Log complaints, assign owners, track case status, flag approaching and overdue deadlines, and preserve timestamped change history |
| Website role | Support and operations case queue, assignment, resolution, and audit history |
| Mobile role | Customer submits and tracks a complaint |
| Synthetic data | Complaint ID, customer alias, transaction reference, category, owner, status, creation time, response due time, resolution time, change events |
| Demo sequence | Submit complaint on mobile → assign on web → advance a controlled demo clock → show deadline warnings → resolve → inspect history |
| Value measures | Assignment time, overdue case count, resolution time |
| Acceptance focus | Correct overdue flags and timestamped history for case changes |
| Proposed edge cases | Exact deadline boundary; unassigned case; closed case after its deadline; reassignment without losing history |
| Main risk | Becomes generic ticketing unless the failed-transfer workflow and handoffs are explicit |
| Boundaries | No live bank integration or automated reversal; deadline rules must be explicitly defined for the demo, not presented as regulatory advice |
| Open questions | What deadline policy applies? Are response and resolution deadlines different? Are deadlines calendar-based or business-hour-based? |
| Status | Proposed; not selected |

## FSI-002 — SettleCheck

| Field | Recorded idea |
|---|---|
| Theme | Payment Reconciliation Tool |
| Problem | A merchant's transaction records disagree with a payment provider's settlement export, requiring manual checks |
| Target users | Merchant finance staff and payment-operations analysts |
| Proposed MVP | Import two files, match transaction ID plus amount, queue duplicates and mismatches, surface missing payments, and prevent duplicate creation on re-import |
| Website role | File import, reconciliation results, and exception review |
| Mobile role | Proposed: merchant views reconciliation summaries and outstanding exceptions; not yet agreed |
| Synthetic data | Source record ID, transaction ID, merchant alias, amount, currency, transaction date, settlement date, import identity |
| Demo sequence | Import transaction and settlement files → match records → inspect missing payments, duplicates, and amount mismatches → re-import → verify unchanged record counts |
| Value measures | Manual checks avoided, unmatched payment value, reconciliation time |
| Acceptance focus | Missing payments surface; re-import adds no duplicates |
| Proposed edge cases | Duplicate within a file versus repeated file import; same ID with conflicting amounts; missing ID; late settlement; different currencies |
| Main risk | Settlement fees, batch payouts, and timing differences can create false exceptions or expand scope |
| Boundaries | Start with a declared synthetic one-to-one settlement model and comparable amounts; do not label unsettled value as confirmed loss or claim real-provider compatibility |
| Open questions | Is the target user merchant finance or a payment provider? Are amounts gross or net? When is a payment genuinely overdue rather than pending? |
| Status | Proposed; assistant's initial preferred option, not a user decision |

## FSI-003 — LoanReady

| Field | Recorded idea |
|---|---|
| Theme | Loan Document Completeness Checker |
| Problem | Borrowers and relationship managers repeatedly exchange documents because requirements vary by loan product and applicant type |
| Target users | Borrower, relationship manager, loan-operations reviewer |
| Proposed MVP | Apply a product-specific checklist to synthetic document metadata and explain missing, outdated, and complete items |
| Website role | Relationship manager selects product and applicant profile, reviews checklist, and tracks readiness |
| Mobile role | Proposed: borrower views outstanding requirements and updates simulated metadata; not yet agreed |
| Synthetic data | Application ID, product, applicant type, document type, issue date, expiry date where applicable, checklist requirement, metadata status |
| Demo sequence | Select mortgage product → check document metadata → explain missing or outdated items → update metadata → show complete readiness |
| Value measures | Document-review time, resubmission rounds, complete application count |
| Acceptance focus | Correct missing / expired / complete classification; no credit decision |
| Proposed edge cases | Optional document absent; document without an expiry requirement; exact expiry boundary; applicant type changes the checklist |
| Main risk | Incorrect checklist or validity assumptions undermine the readiness result |
| Boundaries | Metadata checks only; no OCR, document-authenticity verification, credit scoring, or loan approval |
| Open questions | Which mortgage product and applicant types? Which validity rules are appropriate for each document type? Who owns the checklist? |
| Status | Proposed; not selected |

## FSI-004 — ClaimLens

| Field | Recorded idea |
|---|---|
| Theme | Insurance Claim Fraud Detection |
| Problem | Reviewers need to identify reused invoices, repeated claims, and unusually high amounts without treating every exception as fraud |
| Target users | Claims reviewers and investigation supervisors |
| Proposed MVP | Apply fixed rules, show the evidence and related records behind each flag, and let a reviewer clear or escalate the flag with a reason |
| Website role | Review queue, rule explanations, related-claim comparison, and decision history |
| Mobile role | Proposed: reviewer checks assigned flags and records review outcomes; not yet agreed |
| Synthetic data | Claim ID, policy alias, claimant alias, provider ID, invoice reference, service date, submission date, amount, rule outcomes, reviewer decision |
| Demo sequence | Import claims → inspect reused-invoice, repeat-claim, and high-amount flags → clear a legitimate repeat → escalate a suspicious case with reasons |
| Value measures | Review time, flagged-case workload, false positives on labeled synthetic data |
| Acceptance focus | Explain every flag; human reviewer confirms or clears it |
| Proposed edge cases | Different providers use the same invoice number; legitimate recurring treatment; high-value legitimate claim; repeat import versus a distinct repeat claim |
| Main risk | Overly broad rules produce false positives and unnecessary investigations |
| Boundaries | No ML, OCR, or live integrations; flags are not proof of fraud; no automatic claim rejection |
| Open questions | Which insurance product? What fields establish invoice identity? What repeat window and amount thresholds should the synthetic rules use? |
| Status | Proposed; not selected |

## FSI-005 — Multifinance Verification Orchestrator

### Concept summary

| Field | Recorded idea |
|---|---|
| Origin | User-proposed on 2026-11-16; BR-002 |
| Company | PT Ajukan Kredit Yuk — name supplied by the user on 2026-11-16 in BR-003; legal registration or production operating status has not been independently verified |
| Working title | Multifinance Verification Orchestrator — assistant-proposed descriptive title, not final branding |
| Theme | Multifinance / lending operations; adjacent to LoanReady, but a distinct, broader idea |
| Business objective | Increase sales by reducing verification bottlenecks; any effect on sales remains a hypothesis to measure |
| User-reported pain | Credit applications require multiple document and direct-customer checks, creating bottlenecks and exposure to human error or bias |
| Target users | Verification operations team, individual applicants/borrowers, and corporate customers through their representatives |
| Core concept | Bring sales-originated cases into a verification system; let operations select cases and choose AI-assisted WhatsApp verification or manual calls; compare responses and document data with records; track progress and produce classified results, summaries, and sentiment |
| Existing data source | Reference verification data is already held in the user's verification system; exact schema and API contracts are not yet supplied |
| Proposed MVP scope | Not selected; full-concept capture only, with a separate possible hackathon adaptation below |
| Website role | Operations queue, filters, case selection, channel selection, status tracking, and verification results |
| Customer/mobile role | WhatsApp conversation and document upload; a separate mobile app has not been requested for this concept and WhatsApp may not satisfy the challenge's mobile-app requirement |
| Demo story | Sales creates a case → operations selects one or multiple pending cases → chooses WhatsApp or manual call → verifies application and, later, receipt → reviews evidence, outcome, summary, and sentiment |
| Proposed value measures | Median and upper-percentile verification turnaround; queue age; completed cases per reviewer; human-review rate; correction/rework rate; customer abandonment; sales conversion measured separately |
| Main risks | Wrong-recipient disclosure; sensitive-document exposure; extraction errors; unauthorized API use; ambiguous replies; unfair treatment; duplicate outreach; confusing completion with credit approval or disbursement |
| Status | User-proposed concept; visual, BRD v0.1, PRD v0.1, and TRD v0.1 drafts created on request through BR-005; no requirements sign-off, final stack/vendor selection, or implementation approval |

English terminology: use "applicant / borrower" for the customer's role. The user's term "calon kreditur" is preserved in the conversation record; "creditor" in English normally refers to the lender.

### User-stated capabilities

| ID | Requirement stated by the user |
|---|---|
| FSI-005-U01 | Sales-originated applications enter the verification system and have trackable status changes from pending toward "distributed / selesai verifikasi" |
| FSI-005-U02 | Support individual and corporate customers, with different verification questions |
| FSI-005-U03 | Ask whether the customer really applied for credit; if yes, verify customer identity and application data |
| FSI-005-U04 | Ask whether the customer really received the credit benefit; if yes, verify identity and receipt of a unit or funds |
| FSI-005-U05 | Use verification reference data already stored in the verification system |
| FSI-005-U06 | Request official documents through WhatsApp, such as KTP and SIUP or NIB as applicable; automatically scan/extract and compare identity data |
| FSI-005-U07 | Let operations select one pending case, several cases, all cases, or cases matching their criteria |
| FSI-005-U08 | Let operations choose WhatsApp or manual call for selected cases |
| FSI-005-U09 | AI-assisted WhatsApp sends messages and conducts the verification question-and-answer session automatically |
| FSI-005-U10 | Compare each required data item through APIs, including ICR-assisted KTP checks; specific API providers and authoritative sources are not yet named |
| FSI-005-U11 | Classify whether all details match, some details match, or the contact is wrong; a complete taxonomy is still to be defined |
| FSI-005-U12 | Produce a session summary and sentiment output |
| FSI-005-U13 | Capture the idea now and create a visual flow with English explanations; defer further brainstorming until later |

### Two separate verification stages

| Stage | Business question | What is checked after confirmation | Trigger / boundary |
|---|---|---|---|
| A — Application verification | "Did you apply for this financing?" | Applicant or company identity and application details | Sales/application entry into the verification system |
| B — Receipt verification | "Did you receive the financed unit or funds?" | Recipient identity and actual unit/fund receipt details | Proposed trigger: an independently recorded delivery/disbursement event; exact source and timing are open |

Stage A completion does not approve credit or release money. Stage B must not be asked as if receipt already occurred just because Stage A passed. A customer denying application or receipt creates an exception for investigation, not an automatic rejection or a fabricated confirmation.

### Proposed operational flow — not yet an approved specification

1. **Create or update a case:** link the application, customer type, reference data, current stage, and pending status.
2. **Build the daily worklist:** operations filters and selects one, several, all, or matching eligible pending cases; exact filter fields and the meaning of "all" remain open.
3. **Choose the channel:** AI-assisted WhatsApp or a human-operated manual call; each selected case retains its own session and result.
4. **Apply contact and privacy safeguards:** confirm intended recipient and willingness to continue using an approved low-disclosure process before requesting sensitive documents or revealing application details; exact authentication and consent policy require design.
5. **Ask the stage's confirmation question:** application confirmation for Stage A; receipt confirmation for Stage B. Denial, wrong contact, or refusal stops the sensitive automated questioning and routes the case appropriately.
6. **Collect and check evidence:** request only applicable official documents; use ICR to extract fields; compare with the verification system and authorized API sources. Manual-call cases still need the same evidence requirements through an approved collection process; that process is unresolved.
7. **Ask the correct question set:** individual versus corporate, and application versus receipt. Record answers and field-level comparison results.
8. **Produce results:** keep session status, business-verification outcome, and technical/extraction errors separate; generate summary and descriptive sentiment where a usable conversation exists.
9. **Route exceptions:** incomplete evidence, conflicting data, unclear answers, or low-quality extraction go to human review or follow-up rather than an automatic adverse credit decision.
10. **Complete the current stage:** retain timestamped evidence and review history. Receipt verification is triggered separately after a delivery/disbursement event. Closing policy and any automatic completion of all-matched cases remain open.

### Customer-specific questions — illustrative, not approved scripts

| Customer type | Application-stage examples | Receipt-stage examples | Document considerations |
|---|---|---|---|
| Individual | Did you apply? Confirm identity and the recorded financing request, such as product/unit and amount | Did you receive the unit/funds? Confirm recipient and recorded receipt details, such as unit or amount and date | KTP as proposed by user; required fields and safe document handling still need definition |
| Corporate | Did the company apply? Confirm company identity, representative authority, and the recorded financing request | Did the company receive the unit/funds? Confirm authorized representative and recorded delivery/disbursement details | SIUP or NIB as applicable, with representative identity/authority evidence to be defined; no blanket assumption that every company must supply both |

### Proposed status and result model

The user's original endpoint "distributed / selesai verifikasi" is ambiguous: it may refer to assignment, disbursement, or verification completion. Do not implement it as a synonym without clarification.

| Dimension | Proposed values / behavior |
|---|---|
| Verification stage | Application / Receipt |
| Session progress | Pending → Queued → Contacting → In progress → Awaiting customer or evidence → Under review where needed → Completed |
| Field comparison | Match / Mismatch / Missing or unclear / Not checked |
| Business outcome | All required details matched / Partial or incomplete / Confirmed mismatch / Wrong contact / Customer denies application / Customer denies receipt / Declined verification |
| Contact or technical state | No response / Delivery failed / Extraction uncertain / API unavailable; never silently convert these into a business mismatch |
| Financing lifecycle | Approval, delivery, and disbursement remain external business events, not verification-system decisions |
| Completion | A session may be completed with an exception result; "Completed" does not automatically mean "Verified" or "Disbursed" |

"Partial match" must retain field-level evidence so a missing answer cannot be confused with a confirmed contradiction. Wrong contact is not itself proof of fraud. Sentiment is descriptive only, not a reliability, honesty, or creditworthiness score.

### Result package

- Case, customer type, stage, channel, owner, timestamps, and session/attempt identity.
- Questions asked, answers received, document references, extracted values, source values, and field-level comparison reasons, with sensitive identifiers masked in ordinary views.
- Comparison classification and explanation, unresolved items, and technical-check status.
- Factual summary linked to recorded evidence; AI-generated text must not invent missing answers or override source records.
- Sentiment such as positive, neutral, negative, or uncertain; "not assessed" when no usable conversation exists. Human-authored manual-call notes must not be presented as an AI-analyzed transcript unless one actually exists and its use is authorized.
- Human review/override and follow-up history where applicable.

### Proposed safeguards and limitations

These are assistant recommendations, not user-approved controls or a legal-compliance determination.

- Do not expose sensitive application details to an unconfirmed recipient or use full identity values as an outbound prompt.
- Define document consent/lawful basis, access controls, masking, storage and retention before handling real KTP or corporate documents; keep the hackathon synthetic.
- Confirm that the WhatsApp provider and each verification API are approved and authorized for the intended use; do not assume access to official identity or corporate registries.
- ICR extracts text; it does not establish document authenticity, prove the sender owns the identity, or establish a corporate representative's authority by itself.
- Log matching rules and their versions; provide review and correction paths. Automation may standardize checks but does not guarantee reduced bias.
- Do not use sentiment or document ambiguity to approve or reject financing automatically.
- Avoid duplicate outreach and concurrent active sessions when staff select overlapping batches; proposed operational edge case, not implemented functionality.

### Full concept versus potential hackathon adaptation

| Capability | User's full concept | Possible slide-compatible demo — not yet selected |
|---|---|---|
| Conversation | AI-driven WhatsApp Q&A | Scripted in-app conversation with fixed questions; clearly labeled simulation |
| Official documents | Customer uploads, ICR extraction, identity matching | Synthetic document metadata in CSV/JSON; no scanning or OCR/ICR |
| Reference checks | Existing system plus authorized live APIs | Local synthetic reference records and fixed matching rules |
| Summary | AI-generated session summary | Template populated from recorded answers and rule outcomes |
| Sentiment | AI-generated sentiment description | Omit or use pre-labeled synthetic fixture values clearly marked as mock, not inferred sentiment |
| Manual call | Staff performs and documents the call | Staff records a simulated call outcome |
| Receipt event | Actual unit delivery or fund disbursement event | Explicit simulated event before Stage B |
| Decision boundary | Verification support; approval policy not specified | No credit approval, rejection, or fund release |

The original slide prohibits ML, OCR, and live integrations. Therefore the full concept is not compliant with those constraints as written. Even a simulated version extends beyond the slide's narrow document-completeness checker; facilitator acceptance of the broader workflow remains open. No scope expansion has been approved.

### Open questions for the next brainstorm

| ID | Question | Why it matters |
|---|---|---|
| FSI-005-Q01 | What exactly does "distributed" mean: assigned to staff, disbursed/delivered, or verification finished? | Prevents incorrect status transitions |
| FSI-005-Q02 | What triggers receipt verification, and can application verification ever occur after disbursement? | Defines event timing and stage independence |
| FSI-005-Q03 | Which fields, official documents, and questions are mandatory for each customer type and stage? | Defines completeness and matching rules |
| FSI-005-Q04 | Which source APIs exist, what may they legally return, and what establishes recipient identity and corporate authority? | Separates extraction, internal matching, and authoritative verification |
| FSI-005-Q05 | Which outcomes can be finalized automatically, and which require human review? | Defines accountability and exception ownership |
| FSI-005-Q06 | What are the allowed contact windows, retry limits, opt-out rules, and document-retention policy? | Defines safe operation and customer experience |
| FSI-005-Q07 | Does manual call use WhatsApp for documents or another approved upload route, and is it notes-only or recorded? | Prevents evidence gaps and unsupported sentiment analysis |
| FSI-005-Q08 | Must we follow the slide strictly, or may the team propose AI, ICR, and live integration beyond it? | Determines feasible and acceptable hackathon scope |
| FSI-005-Q09 | What current turnaround, rework, abandonment, and sales-conversion baselines are available? | Enables a defensible business-value claim |

### BRD readiness — BR-003, 2026-11-16

| Area | Assessment / proposed treatment |
|---|---|
| Readiness | Enough information for BRD v0.1 — Draft for Discussion; not yet sufficient for a signed-off requirements baseline |
| Known business context | Company name, sales-growth objective, verification bottleneck, human-error/bias concern, target users, and existing reference-data system |
| Known capability outline | Two verification stages, individual/corporate question sets, daily queue and batch selection, WhatsApp/manual channels, document and API comparisons, classifications, summary, and sentiment |
| Business rules to clarify | Meaning of distributed; stage triggers; mandatory questions/documents; matching and completion rules; review/override authority; exception ownership |
| Success measures to clarify | Baseline and target turnaround, SLA, throughput, rework, and sales-conversion metrics; benefit figures must not be invented |
| Data and governance to clarify | Recipient verification, consent/lawful basis, access and retention, approved data sources, business owner, and sign-off responsibilities |
| Scope decision | Distinguish the full business concept from a permitted hackathon implementation; real AI, ICR, and live integrations remain outside the slide's stated constraints |
| Drafting recommendation | Start a discussion draft with explicit assumptions and TBD items linked to the open-question IDs; do not convert proposals into approved requirements |
| Technical detail boundary | API payloads, architecture, and implementation design can be elaborated in PRD/TRD; missing technical details need not prevent the initial business draft |
| Authorization / artifact state | User asked whether the concept is ready for a BRD; no BRD file has been created in this round, and no sign-off or implementation approval has been inferred |

### BRD deliverable — BR-004, 2026-11-16

| Area | Recorded outcome |
|---|---|
| Authorization | User explicitly requested the verification BRD for PT Ajukan Kredit Yuk, then repeated the request with Karpathy Guidelines; this authorizes drafting, not implementation or sign-off |
| Artifact | [BRD PT Ajukan Kredit Yuk — Verifikasi v0.1](file:///Users/rizkyazhary/Documents/Cakra/rizky-di-cakra/Qoder-BFSI-Initiatives/01_documents/01_brd/BRD_PT_Ajukan_Kredit_Yuk_Verifikasi_v0.1.docx) |
| Document identity | AKY-BRD-VER-001; Indonesian; v0.1 — Draft untuk Pembahasan |
| Coverage | Two verification stages, individual/corporate profiles, WA/manual channels, documents/ICR/API checks, classifications, summaries, sentiment, review and safeguards |
| Structure | 13 main sections; 20 business requirements, 10 proposed business rules, 7 proposed NFRs, 19 proposed acceptance scenarios, 5 assumptions, and 13 open decisions |
| Traceability | BR-01–BR-16 elaborate U01–U12; BR-17–BR-20 are proposed controls. U13 is the documentation request, not an application feature. D-01–D-09 link to existing Q01–Q09; D-10–D-13 add explicit governance, capacity, batch-selection, and taxonomy questions |
| Scope status | Full business concept recorded separately from the unselected hackathon simulation; no vendor, numeric performance target, mandatory evidence policy, or finalization authority invented |
| Verification | Document content read back; structural check found only intentional TBD placeholders and pending TOC page numbers. Save/reopen succeeded. Read-only saved-DOCX checks confirmed 25 tables, expected unique IDs and explicit reference resolution, required content, A4 page size, and well-formed header/footer XML |
| Limitations | Visual pagination was not reviewed; update TOC fields in Word. The 19 acceptance scenarios are proposed tests, not executed application tests |
| Next step | Business review of open decisions, beginning with distributed status, receipt trigger, mandatory evidence/questions, review authority, privacy/contact policy, and full-concept versus hackathon scope |

The BR-003 readiness assessment above is preserved as a historical record of the earlier round; BR-004 records the later drafting authorization and saved artifact. This register remains the brainstorm record; the Word file is an unapproved requirements draft.

### PRD and TRD deliverables — BR-005, 2026-11-16

| Area | Recorded outcome |
|---|---|
| Authorization | User requested PRD and TRD after the BRD; drafting is authorized, not implementation, production deployment, or requirements sign-off |
| PRD | [AKY-PRD-VER-001 v0.1](file:///Users/rizkyazhary/Documents/Cakra/rizky-di-cakra/Qoder-BFSI-Initiatives/01_documents/02_prd/PRD_PT_Ajukan_Kredit_Yuk_Verifikasi_v0.1.docx); Indonesian discussion draft, 17 product requirements/user stories, 7 proposed screens, 17 product acceptance scenarios |
| TRD | [AKY-TRD-VER-001 v0.1](file:///Users/rizkyazhary/Documents/Cakra/rizky-di-cakra/Qoder-BFSI-Initiatives/01_documents/03_trd/TRD_PT_Ajukan_Kredit_Yuk_Verifikasi_v0.1.docx); Indonesian proposed technical design, 12 technical requirements, 14 internal API contracts, 12 proposed technical tests, 6 open technical decisions |
| Product elaborations | Frozen batch-preview target membership with revalidation at dispatch; explicit partial/conflict results; recipient gate; stage-specific checklists; source/evidence version visibility; human finalization as a conservative proposal pending D-05 |
| Technical recommendations | Modular monolith; React/TypeScript UI; Node.js LTS/TypeScript/Fastify API and worker; PostgreSQL with durable inbox/outbox; private storage and OIDC/SSO if available. These are proposals awaiting review, not selected vendors or installed dependencies |
| Reliability and safety | Separate case progress from contact/confirmation/match/technical states; idempotency and unique active attempt; reconcile DELIVERY_UNKNOWN rather than blind resend; quarantine documents; object authorization; version-aware checks/review; constrain AI to evidence-backed outputs, not credit decisions |
| Source preservation | BRD v0.1 remains unchanged. D-01–D-13 remain open; technical decisions T-01–T-06 make the additional design choices explicit |
| Verification | Both DOCX files saved and read back. Structural checks found only intentional placeholder/TBD warnings. Read-only package/reference checks verified all 20 BR map to PR, all 17 PR map to TR, unique definition counts, explicit/slash ID references, 10 PRD tables, 13 TRD tables, and consistent 14 API contracts |
| Limits | No application, API, UI, security or performance test was executed; test scenarios are proposed. Visual pagination/layout remains unverified. Full versus hackathon scope and mobile-app expectations are still unresolved |
| Next step | Review product behavior and technical recommendations, resolve business/technical blockers, then authorize any implementation separately |

### Visual companion

[English concept flow and explanations](file:///Users/rizkyazhary/.qoder/projects/-Users-rizkyazhary-Documents-Cakra-rizky-di-cakra-Qoder-BFSI-Initiatives/canvases/multifinance-verification-flow.canvas.tsx) — companion artifact; concept visualization only, not an implemented integration. This register is the authoritative brainstorm record.

## Initial comparison and recommendation

These are qualitative assistant judgments, not validated scoring results.

| Evaluation angle | Initial view | Tradeoff |
|---|---|---|
| Best balance of feasibility and financial-value demonstration | FSI-002 — SettleCheck | Clear reconciliation outcome, but settlement assumptions must stay narrow |
| Safest complete build | FSI-001 — Complaint Rescue | Simpler workflow, but differentiation depends on realistic operational handoffs |
| Clearest checklist-oriented workflow | FSI-003 — LoanReady | Easy to explain, but business credibility depends on correct checklist rules |
| Most distinctive investigation story | FSI-004 — ClaimLens | Compelling evidence-based demo, but false positives and human review need careful treatment |

## Decisions and unresolved questions

| ID | Type | Record | State |
|---|---|---|---|
| DEC-001 | User instruction | Persist every brainstorm in a structured form | Confirmed 2026-11-16 |
| REC-001 | Assistant recommendation | Prefer SettleCheck for feasibility plus demonstrable financial value | Historical BR-001 recommendation; not adopted; BR-002 focus moved to user-proposed FSI-005 |
| DEC-002 | User request | Record FSI-005 and create an English visual flow; continue brainstorming later | Confirmed 2026-11-16; not approval to build or deploy |
| DEC-003 | User-provided company name | PT Ajukan Kredit Yuk is the company name for FSI-005 | Confirmed by user 2026-11-16; no external legal verification implied |
| REC-002 | Assistant recommendation | Sufficient context for BRD v0.1 — Draft for Discussion; retain unresolved rules and scope as assumptions/TBD | Proposed in BR-003; drafting subsequently authorized in DEC-004, not requirements sign-off |
| DEC-004 | User request | Create the verification BRD for PT Ajukan Kredit Yuk; repeated with Karpathy Guidelines | Confirmed 2026-11-16; v0.1 saved in BR-004, still a discussion draft; no application implementation or external publication authorized |
| DEC-005 | User request | Create PRD and TRD from the verification BRD | Confirmed 2026-11-16; both v0.1 drafts saved in BR-005; product/technical proposals are not signed off and implementation remains unauthorized |
| Q-001 | Selection criterion | Optimize for the strongest business pitch, safest complete build, or most distinctive demo? | Open; asked in conversation |
| Q-002 | Delivery constraints | What are the team size, available time, and budget? | Open; not yet discussed |
| Q-003 | Challenge interpretation | Confirm mobile-app expectations and whether the slide's Sonus requirement applies unchanged | Open; not yet discussed |
| Q-004 | Business validation | Which target users or domain experts can validate the chosen workflow? | Open; not yet discussed |

## Round log

| Round | Date | Input | Ideas / changes | Outcome |
|---|---|---|---|---|
| BR-001 | 2026-11-16 | User supplied four FSI hackathon themes and requested practical use-case brainstorming | Proposed FSI-001 through FSI-004; compared feasibility, value, and demo appeal | SettleCheck recommended by assistant; no user selection |
| Register setup | 2026-11-16 | User requested structured recording for every brainstorm | Backfilled all four ideas, constraints, recommendation, and open questions; added explicitly provisional data, edge-case, and mobile-role details | Register established; recording preference saved |
| BR-002 | 2026-11-16 | User described multifinance sales bottlenecks and proposed AI-assisted customer/document verification; requested recording and an English visual, with further brainstorming deferred | Added FSI-005, 13 user-stated capabilities, two verification stages, channel branches, proposed status/result dimensions, safeguards, scope comparison, and nine open questions | FSI-005 is current discussion focus; no production build, final hackathon selection, or automatic credit decision authorized |
| BR-003 | 2026-11-16 | User asked whether the concept is sufficient for a BRD and supplied PT Ajukan Kredit Yuk as the company name | Recorded company name, drafting-readiness assessment, remaining business-rule/governance gaps, and recommendation to use explicit assumptions/TBD | Enough for a discussion draft, not sign-off; BRD drafting not yet undertaken |
| BR-004 | 2026-11-16 | User requested the verification BRD, interrupted the first attempt, then repeated the request with Karpathy Guidelines | Created and saved Indonesian Word BRD v0.1 with requirement/acceptance traceability, explicit assumptions and open decisions; checked document structure and saved-file integrity | Discussion draft saved for business review; no production implementation, sign-off, or application test execution; visual pagination unverified |
| BR-005 | 2026-11-16 | User requested PRD and TRD | Created Indonesian PRD/TRD v0.1 with product stories/screens, proposed architecture/data/API/security/reliability design, test traceability and explicit open decisions; verified every BR-to-PR and PR-to-TR mapping | Two drafts saved for review; original BRD unchanged; no implementation, final scope/stack approval, live integration, or application test execution |
