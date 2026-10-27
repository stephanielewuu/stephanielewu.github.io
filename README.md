# Team Charter: Cogent Support Engineering & Platform Optimization
### 1. Purpose & Mission
Transform Cogent's Managed Service Provider (MSP) support operations by eliminating queue bottlenecks, formalizing end-to-end inbound ticket routing, enforcing clear SLAs, and restoring client service excellence within the Gorgias support platform.

### 2. Core Values
- **Operational Clarity & Ownership:** Eradicate passive ticket assumption; enforce unambiguous lead assignment across every open issue.
- **Client Transparency:** Maintain continuous communication cadences so clients never experience communication blackouts.
- **Knowledge Retention:** Transform recurring fixes and routine disruptions into shared, documented runbooks to liberate senior engineering capacity.
- **Delivery Integrity:** Respect scheduled sprint timelines by actively defending developer focus against unscheduled side-channel requests.

### 3. Working Agreements
- **Triage Cadence:** Daily queue inspection and triage alignment within 2–4 business hours of inbound ticket creation.
- **Resourcing & Coverage Mandate:** Every functional squad maintains at least one developer on active standby to service incoming tickets (utilizing weekly rotations, dedicated pairs, or an assigned point person).
- **Communication Cadence:** Post documented client status updates on all active tickets every 24–48 hours until closure.
- **Definition of Done (DoD) for Support Tickets:**
  * Root cause diagnosed and resolved in production.
  * Solution verified with the client via Gorgias.
  * For recurring issues or environment maintenance (e.g., Medscheme server patching), client runbook/knowledge base entry updated or verified.
  * Ticket formally marked as closed in Gorgias with complete tagging.
- **Communication Protocols:** Stop all side-channel interactions (WhatsApp, direct email); funnel 100% of issues to `support@cogent` or the Client Portal.

### 4. Operational Boundaries & Escalation Protocols
- **Capacity Clashes:** When an urgent ticket conflicts with active sprint commitments, the Account Lead engages the client immediately to evaluate priority: *"We see this request; how does this rank in priority compared to what we are currently building?"*
- **Scope Escalation:** Mid-sprint scope changes, unplanned design reworks, or urgent client requests exceeding team bandwidth must be escalated to senior leadership to negotiate formal change requests.
- **Stagnation Trigger:** Any ticket remaining unassigned or static for >72 hours (3 business days) triggers automated escalation alerts to the Account Lead and Operations Lead.

### 5. Reflection
The Agile Team Charter directly addressed the critical operational deficits revealed in our Gorgias Readiness Survey ($N=6$). Prior to this agreement, 83.3% of the team reported falsely assuming a colleague was covering a ticket, and 50% reported unclear individual ownership. Establishing explicit standby coverage options (rotations, pairs, or designated point persons) eliminated ambiguity without disrupting development velocity. Furthermore, defining strict escalation pathways for capacity clashes gave the engineering team a structured mechanism to defend sprint commitments while maintaining responsive, transparent client communication.

---

# 2. User Stories and Tasks

### Evidence (Artifact)

#### Story US-01: Centralized Ingestion & Instant Auto-Acknowledgment
> **As a** Cogent Client,  
> **I want** to receive an immediate confirmation with a reference ID when submitting an issue to `support@cogent`,  
> **So that** I know my request has entered the support queue and panic escalations to management are prevented.

* **Acceptance Criteria:**
  1. Emails to `support@cogent` generate a ticket in Gorgias within 2 minutes.
  2. Automated confirmation response dispatches back to the client with a unique Ticket ID and an SLA overview.
  3. Side-channel communications redirected to the central support desk.
* **Engineering Tasks:**
  - [x] **TASK-201:** Configure Gorgias inbound mail parser for `support@cogent` and client portal webhooks.
  - [x] **TASK-202:** Draft and implement automated acknowledgment macro template containing ticket reference and SLA expectations.
  - [x] **TASK-203:** Draft standard macro response for team members to redirect client WhatsApp and personal email requests to `support@cogent`.

#### Story US-02: Account Lead Triage, Tagging, and Lead Steering
> **As an** Account Lead,  
> **I want** inbound tickets categorized with structured tags and routed to the responsible dev or infra lead within 2–4 hours,  
> **So that** tickets do not sit idle in unmonitored queues without designated ownership.

* **Acceptance Criteria:**
  1. Gorgias rule tags inbound tickets by client domain and infrastructure category.
  2. Account Lead reviews stack traces and assigns explicit individual ownership within 4 hours.
  3. Work requests outside bug fixes are flagged as Change Requests.
* **Engineering Tasks:**
  - [x] **TASK-204:** Establish unified tag schema (Client ID, Bug vs Change Request, Infrastructure vs App).
  - [x] **TASK-205:** Build custom Gorgias views segmented by squad assignment and unassigned status.
  - [x] **TASK-206:** Configure 72-hour inactivity warning notifications sent to the Operations Lead.

#### Story US-03: Client Cadence Updates & Runbook Retention
> **As an** Assigned Developer,  
> **I want** pre-formatted Gorgias update macros and runbook templates,  
> **So that** I can maintain a 24–48 hour communication cadence and document recurring environment fixes.

* **Acceptance Criteria:**
  1. Tickets pending longer than 24 hours prompt the developer for a progress update.
  2. Resolved recurring issues require a verified link to the internal Knowledge Base before closing.
* **Engineering Tasks:**
  - [x] **TASK-207:** Build progress-update macro templates for ongoing investigations.
  - [x] **TASK-208:** Create environment runbook documentation repository for recurring procedures (e.g., Medscheme bi-weekly server restart runbook).

### Reflection
Survey findings indicated that 50% of the team found previous tagging and sorting ineffective, while 83.3% struggled to detect urgent queries. Deconstructing these issues into targeted user stories bridged user-facing expectations and internal queue mechanics. Framing triage as an Account Lead responsibility with explicit time targets (2–4 hours) solved the fundamental ownership void. Additionally, breaking down tasks into operational templates (such as side-channel redirects and recurring runbook checklists) lowered platform friction, driving up daily adoption across engineering teams.

---

# 3. Product Backlog

### Evidence (Artifact)

| Priority | ID | Item Description | Category | Est. (Story Points) | Target Milestone |
| :---: | :---: | :--- | :--- | :---: | :---: |
| **Must** | PB-01 | Configure centralized funnel routing (`support@cogent` / Client Portal) with <2 min automated confirmation dispatches | Ingestion & Core SLA | 3 | Sprint 1 |
| **Must** | PB-02 | Build triage queue views and tagging architecture (Client ID, Category, Bug vs Change Request) | Triage Engine | 5 | Sprint 1 |
| **Must** | PB-03 | Set up automated 72-hour stagnation alert rules notifying Account and Operations Leads | SLA & Escalation | 5 | Sprint 1 |
| **Must** | PB-04 | Establish team standby rota configuration (weekly rotations, pairs, or point person tracking) | Operations Governance | 3 | Sprint 1 |
| **Should**| PB-05 | Implement standardized 24–48 hour client update macros and side-channel redirect macros | Client Experience | 3 | Sprint 2 |
| **Should**| PB-06 | Build Knowledge Base / Runbook integration for recurring maintenance (e.g., Medscheme patching) | Knowledge Retention | 8 | Sprint 2 |
| **Could** | PB-07 | Implement employee onboarding walkthrough sessions for team-by-team Gorgias platform adoption | Training & Enablement | 5 | Sprint 2 |
| **Won't**  | PB-08 | Autonomous AI-driven issue auto-resolution (Deferred to mature Phase 2 KB rollout) | Advanced AI | 13 | Post-MVP |

### Reflection
The MoSCoW prioritization model ensured the platform maturation tackled core operational risks before introducing advanced tooling. Survey insights showed 0% daily platform usage and 60% of delays caused by competing sprint commitments. Prioritizing auto-acknowledgments and stagnation alerts in Sprint 1 directly protected client trust while giving leadership visibility over lingering work. Less urgent initiatives—such as deep knowledge base integrations and training walkthroughs—were sequenced into subsequent sprints, ensuring technical stabilization preceded broader procedural rollout.

---

# 4. Sprint Backlog

### Evidence (Artifact)

* **Sprint Goal:** Deploy Gorgias ingestion automation, establish the 2–4 hour Account Lead triage pipeline, and activate the 72-hour stagnation warning engine.
* **Sprint Duration:** 2 Weeks (Sprint 1)
* **Committed Points:** 16 Story Points
* **Velocity / Burndown Status:** 6 points completed, 10 points active in testing/review.

```
+-----------------------------------------------------------------------------------------------+
|                                      SPRINT 1 KANBAN BOARD                                    |
+-------------------+--------------------+----------------------+-------------------------------+
| TO DO             | IN PROGRESS        | IN REVIEW / TESTING  | DONE                          |
+-------------------+--------------------+----------------------+-------------------------------+
| [PB-04] Team      | [PB-03] 72-Hour    | [PB-02] Gorgias Tag  | [TASK-201] Mail parser setup  |
| standby roster    | stagnation alert   | schema and triage    | for support@cogent (3 pts)    |
| setup & pairing   | workflow triggers  | views (5 pts)        |                               |
| agreements        | (5 pts)            |                      | [TASK-202] <2 min automated   |
| (3 pts)           |                    |                      | client confirmation macro     |
|                   |                    |                      | verification (3 pts)          |
+-------------------+--------------------+----------------------+-------------------------------+
```

### Reflection
The Sprint Backlog served as an operational shield, protecting developers from the frequent context switching identified in our employee readiness survey. Visualizing tasks across Kanban swimlanes made team standby resourcing tangible. By actively tracking the stagnation alert rule in Sprint 1, the team converted what was previously an invisible bottleneck (tickets sitting unassigned for days) into an automated alert mechanism, keeping workload distribution transparent between Account Leads and technical squads.

---

# 5. Agile Logbook

### Evidence (Artifact)

#### Daily Stand-up Entries

* **Sprint 1 — Day 3**
  * **Yesterday:** Finalized Gorgias mail parser integration for `support@cogent` and verified that incoming emails trigger an automated acknowledgment within 90 seconds.
  * **Today:** Building triage view filters for Account Leads based on the new tagging taxonomy (Client ID, Bug vs Change Request).
  * **Blockers:** Found several clients still submitting requests via personal developer emails and WhatsApp channels, bypassing Gorgias.

* **Sprint 1 — Day 7**
  * **Yesterday:** Deployed the 72-hour stagnation alert rule in Gorgias test queue to trigger Slack and email alerts to the Operations Lead.
  * **Today:** Validating standby resourcing models across squads (testing the rotating primary vs dedicated pairs structure).
  * **Blockers:** Developers expressed concern that handling ticket triage conflicts with scheduled sprint velocity.

#### Sprint Retrospective Log (Sprint 1 Review)

| What Went Well | What Didn't Go Well | Action Items for Next Sprint |
| :--- | :--- | :--- |
| • Instant confirmation emails (<2 min) eliminated panic follow-ups from clients.<br>• Account Leads successfully triaged 85% of incoming issues within 4 hours.<br>• Centralized funnel stopped unrecorded queue leakage. | • Side-channel requests continued to filter in via personal WhatsApp and email.<br>• Unplanned high-priority tickets disrupted focused sprint development capacity.<br>• Tagging inconsistencies occurred when multiple developers updated the same ticket. | • Deploy standardized redirect macros for team members to steer clients to `support@cogent`.<br>• Enforce the trade-off conversation rule (*"How does this rank against current sprint builds?"*).<br>• Roll out Phase 2 walkthrough and onboarding training sessions across all squads. |

### Reflection
The logbook entries highlight the shift from reactive problem-solving to structured continuous improvement. Standup notes surfaced persistent root causes—such as side-channel requests and mid-sprint capacity clashes—that previously degraded team morale and distorted sprint velocity. Documenting these dynamics in the retrospective led directly to actionable protocols: standardizing client redirect macros and establishing clear capacity escalation rules for Account Leads. This structured feedback loop demonstrated how transparent Agile tracking can systematically resolve operational friction in a fast-paced MSP environment.

