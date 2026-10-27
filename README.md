# Team Charter: Cogent Support Engineering & Platform Optimization

### 1. Purpose & Mission
Modernize and scale Cogent’s support operations by optimizing the Gorgias helpdesk platform, automating ticket categorization, and establishing predictable SLA turnaround times.

### 2. Core Values
- Reliability: Production-first mindset; zero unexpected disruption to live customer tickets.
- Data-Informed: Prioritize automation rules based on ticket volume metrics and audit logs.
- Transparency: Open documentation of all macro changes, triage logic, and tag schemas.

### 3. Working Agreements
- Daily Standup: 09:30 AM SAST (15 minutes, focus on blocker resolution).
- Definition of Done (DoD):
  * Rule/macro tested in staging or sandbox environment.
  * Peer review/approval completed.
  * Documentation updated in team wiki/Gorgias admin guide.
  * SLA tracking tags confirmed operational.
- Communication Channels: Slack for asynchronous blockers; Jira/Trello for task tracking; weekly sync for sprint planning and review.

### 4. Operational Boundaries & Conflict Resolution
- Disagreements on rule routing priority will be resolved using empirical ticket volume analysis.
- Blockers lasting >4 hours must be escalated to the engineering lead immediately.

### 5. Reflection
The creation of the Agile Team Charter was crucial in transitioning platform optimization from reactive maintenance into a disciplined engineering cadence. By standardizing our Definition of Done (DoD) to require staging tests before deploying routing macros to live Gorgias ticket queues, the charter prevented pipeline breakage and misrouted customer queries. It aligned operational boundaries between technical implementation and customer-facing support requirements, minimizing friction and fostering mutual accountability across the engineering and support workflows.

---

# 2. User Stories and Tasks

### Evidence (Artifact)

#### Story US-01: Automated Triage for High-Priority Tickets
> **As a** Tier-1 Support Agent,  
> **I want** urgent billing and account-access tickets automatically tagged and prioritized upon arrival,  
> **So that** critical issues can be resolved within our 1-hour SLA target without manual triage.

- **Acceptance Criteria:**
  1. Gorgias rule triggers on keywords (`payment failed`, `unauthorized`, `account locked`, `urgent`).
  2. The ticket is tagged with `priority:high` and assigned directly to the Urgent Support View.
  3. Escalation notification sends via webhook to the dedicated Slack escalation channel.

- **Engineering Tasks:**
  - [x] **TASK-101:** Audit historical Gorgias ticket search logs to compile high-frequency urgency keywords.
  - [x] **TASK-102:** Configure rule triggers and regex conditions in the Gorgias automation engine.
  - [x] **TASK-103:** Configure webhook payload and verify Slack alert dispatch.
  - [x] **TASK-104:** Run 20 historical mock tickets through sandbox to measure false-positive rate.

#### Story US-02: Macro-Driven Resolution for Common Inquiries
> **As an** Integration Support Engineer,  
> **I want** standardized macro templates pre-populated with API troubleshooting steps,  
> **So that** repeated technical inquiries receive consistent and fast first-contact resolutions.

- **Acceptance Criteria:**
  1. Macros created for top 3 integration error patterns (Auth 401, Rate Limit 429, Webhook Delivery Failures).
  2. Variables (e.g., `{{ticket.customer.name}}`, `{{ticket.id}}`) dynamically inject context.

- **Engineering Tasks:**
  - [x] **TASK-105:** Analyze top 50 technical query tickets from Q2/Q3.
  - [x] **TASK-106:** Draft macro copy with links to documentation and verification checklists.
  - [x] **TASK-107:** Test macro variable rendering across web and email channels.

### Reflection
Deconstructing broad support objectives into structured user stories revealed the critical link between user intent and backend execution. Initially, support requirements were vague (e.g., "improve ticket sorting"). Translating these into formal user stories with strict acceptance criteria forced our team to define exact triggers and measurable boundaries. Breaking stories down into discrete engineering tasks made effort estimation much more realistic, highlighting hidden dependencies like regex testing and webhook latency verification early in the cycle.

---

# 3. Product Backlog

### Evidence (Artifact)

| Priority | ID | Item Description | Category | Est. (Story Points) | Target Milestone |
| :---: | :---: | :--- | :--- | :---: | :---: |
| **Must** | PB-01 | Implement automated auto-tagging rules for incoming tickets by topic (Billing, Tech, General) | Automation | 5 | Sprint 1 |
| **Must** | PB-02 | Build automated SLA warning triggers (flag tickets reaching 75% of breach threshold) | SLA Engine | 8 | Sprint 1 |
| **Must** | PB-03 | Configure Gorgias HTTP integration webhooks to log incident tickets into internal database | Integration | 5 | Sprint 2 |
| **Should** | PB-04 | Standardize Tier-1 technical response macros with dynamic customer variables | Efficiency | 3 | Sprint 2 |
| **Should** | PB-05 | Create Gorgias custom views segmented by SLA urgency and agent team ownership | UX / Workflow | 3 | Sprint 2 |
| **Could** | PB-06 | Implement CSAT survey dispatch workflow upon ticket closure | Analytics | 2 | Sprint 3 |
| **Won't** | PB-07 | Custom AI chatbot integration for full autonomous resolution (Deferred to Phase 2) | R&D | 13 | Post-MVP |

### Reflection
Managing the Product Backlog using the MoSCoW prioritization model highlighted the constant balance between technical capability and business urgency. While advanced automated AI chatbots were appealing, prioritizing core reliability—such as auto-tagging and SLA alert thresholds—was necessary to stabilize baseline operational metrics. Backlog grooming sessions enabled continuous reprioritization as real ticket data arrived, ensuring high-value, low-risk automation items were tackled first.

---

# 4. Sprint Backlog

### Evidence (Artifact)

- **Sprint Goal:** Automate incoming ticket triage and deploy real-time SLA breach prevention rules in Gorgias.
- **Sprint Duration:** 2 Weeks (Sprint 1)
- **Committed Points:** 18 Story Points
- **Velocity / Burndown Status:** 5 points completed, 13 points actively in execution/testing.

```
+-----------------------------------------------------------------------------------------------+
|                                      SPRINT 1 KANBAN BOARD                                    |
+-------------------+--------------------+----------------------+-------------------------------+
| TO DO             | IN PROGRESS        | IN REVIEW / TESTING  | DONE                          |
+-------------------+--------------------+----------------------+-------------------------------+
| [PB-03] Database  | [PB-02] SLA 75%    | [PB-01] Gorgias Tag  | [TASK-101] Keyword audit on   |
| webhook logging   | warning trigger    | automation rule      | historical support tickets    |
| (5 pts)           | setup (8 pts)      | validation (5 pts)   | (2 pts)                       |
|                   |                    |                      |                               |
|                   |                    |                      | [TASK-102] Sandbox regex rule |
|                   |                    |                      | construction (3 pts)          |
+-------------------+--------------------+----------------------+-------------------------------+
```

### Reflection
The Sprint Backlog served as the operational engine for daily execution. Setting a cohesive Sprint Goal prevented scope creep and kept the focus squarely on ticket triage stabilization rather than peripheral configuration. Tracking progress on a visual board made bottlenecks immediately visible—such as tickets spending too long in the "In Review / Testing" lane due to waiting on historical sample verification. This prompted real-time workload balancing during standups to keep tasks moving smoothly.

---

# 5. Agile Logbook

### Evidence (Artifact)

### 1. Daily Stand-up Entries

#### Date: Sprint Day 3
- **Yesterday:** Completed regex pattern construction for billing and account lockout keywords in Gorgias sandbox.
- **Today:** Implementing Gorgias auto-tagging rule conditions and setting ticket priority levels.
- **Blockers:** Found edge-case tickets where customers combined multiple issues in a single email, risking conflicting tags.

#### Date: Sprint Day 6
- **Yesterday:** Resolved tag conflict logic by defining hierarchical rule precedence (Security/Billing > Technical > General).
- **Today:** Testing webhook alerts from Gorgias to Slack for SLA threshold warnings at 75% elapsed time.
- **Blockers:** None currently.

### 2. Sprint Retrospective Log (Sprint 1 Review)

| What Went Well | What Didn't Go Well | Action Items for Next Sprint |
| :--- | :--- | :--- |
| - Rule automation reduced manual triage volume by over 30% in sandbox testing.<br>- Clean, modular rule logic structure. | - Initial keyword matching was too broad, causing false alarms on general billing inquiries.<br>- Sandbox environment data was slightly out of date. | - Add negative keyword exclusions to rules (e.g., exclude "receipt request").<br>- Refresh sandbox data weekly with anonymized ticket samples. |

### Reflection
Maintaining a structured Agile Logbook transformed our team's operational habits from ad-hoc problem solving into measurable continuous improvement. Documenting daily stand-ups highlighted patterns in systemic blockers—such as multi-intent ticket routing conflicts—that would have otherwise been forgotten or repeatedly encountered. The sprint retrospective provided a dedicated space to examine failure points candidly, ensuring that adjustments (like rule precedence and negative keyword exclusions) directly informed the planning of subsequent sprints.
