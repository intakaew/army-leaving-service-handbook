# IT Manager level: service management, operations and delivery management (research report)

Scope: the management/ITSM layer of a large-organisation IT department: service desk, incident/problem/change, postmortems, on-call, SLA/SLO, capacity, release, PMO/portfolio, agile at scale, team management, vendor management, reporting.

Method: searched GitHub for public agent skills (SKILL.md), ranked them by repository stars (skills.sh install counts were unreachable), read the best ones, and distilled the main frameworks. Official framework sites were blocked by the network proxy, so the digests rely on prior knowledge plus the PagerDuty and Google-SRE-book postmortem templates, which were readable through GitHub.

---

## 1. Skills catalog (แคตตาล็อกสกิล)

★ = full SKILL.md read.

| Rank | Repo (stars) | Relevant skills (path) | Verdict |
|---|---|---|---|
| 1 | **anthropics/skills** (~187k) | No ITSM skills; it is the reference for the skill format | Format only |
| 2 | **sickn33/agentic-awesome-skills** (~49k) | ★`plugins/agentic-awesome-skills/skills/it-manager-pro`, ★`skills/incident-management`, `skills/change-management`, `capacity-workload-planner`, `vendor-management`, `vendor-contractor-management`, `risk-manager`, `alerting-oncall`, `slo-implementation`, `pre-release-review`, `hr-pro`, `projects-work-management` | Wide coverage. `incident-management` (18 KB) has a good escalation matrix, war-room procedure and postmortem. `it-manager-pro` is mostly persona text with little procedure. |
| 3 | **wshobson/agents** (~42k) | `plugins/incident-response/skills/`: ★`postmortem-writing`, ★`on-call-handoff-patterns`, `incident-runbook-templates`, `connectivity-triage`. ★`observability-monitoring/skills/slo-implementation` | **Best for SRE practice.** Includes a 5-whys example, a shift-handoff timing pattern, and an error-budget policy ladder. |
| 4 | **anthropics/knowledge-work-plugins** (~35k) | ★`operations/skills/{change-request, status-report, vendor-review, capacity-plan, risk-assessment}`, `operations/skills/{runbook, process-doc, process-optimization}`, ★`engineering/skills/incident-response`, `engineering/skills/{standup, deploy-checklist, tech-debt}`, `product-management/skills/{sprint-planning, stakeholder-update, roadmap-update}`, `human-resources/skills/{org-planning, onboarding, draft-offer}`, `small-business/skills/hiring-screener` | **Best overall for IT managers.** Short, clean output templates and connector hooks for ITSM, project tracker, chat and calendar. Install this first. |
| 5 | **alirezarezvani/claude-skills** (~29k) | ★`engineering-team/skills/incident-commander` (16 KB, stakeholder update-cadence matrix), ★`project-management/skills/senior-pm` (charter, RACI, portfolio reviews), ★`scrum-master` (sprint health scoring), ★`business-operations/skills/vendor-management` (weighted vendor scoring plus SLA-credit scripts), ★`engineering/skills/slo-architect` (burn-rate alerting), `capacity-planner`, `process-mapper`, `c-level-advisor/skills/change-management`, `vpe-advisor`, `chro-advisor`, `runbook-generator`, `tech-debt-tracker`, `ra-qm-team/skills/risk-management-specialist`, `isms-audit-expert` | **Deepest.** Comes with Python scripts for velocity, SLA compliance and vendor risk. |
| 6 | **Jeffallan/claude-skills** (~12k) | `skills/sre-engineer`, `monitoring-expert`, `chaos-engineer`, `atlassian-mcp` | Practitioner-level SRE |
| — | **dastergon/postmortem-templates** (~1.5k) | Not a skill: a collection of postmortem templates (Google SRE book, PagerDuty, Atlassian and others) | Primary-source templates |
| — | **PagerDuty/incident-response-docs** (~1k) | Not a skill: the PagerDuty incident-response handbook (IC, scribe and comms roles, postmortem template) | Primary source, read |
| 7 | borghei/Claude-Skills (~1k) | `project-management/career/pm-1on1s` | — |
| 8 | rampstackco/claude-skills (~1k) | `incident-response`, `after-action-report`, `launch-runbook`, `sprint-operations`, `stakeholder-communication`, `vendor-evaluation`, `backup-and-disaster-recovery`, `okr-design`, `team-onboarding-playbook` | Fills gaps (launch, DR, OKRs) |
| 9 | majiayu000/claude-skill-registry (~700) | `itil-expert`, `dora-metrics`, `one-on-one-prep` | Now only pointers to an archive repo |
| 10 | aj-geddes/useful-ai-prompts (~380), OneWave-AI/claude-skills (~410) | `runbook-creation`, `runbook-generator` | — |
| 11 | nagisanzenin/production-grade (~180), diegosouzapw/awesome-omni-skills (~170) | `sre`, `itil-expert`, `itil-expert-v2` | ITIL-specific |
| 12 | jcesarperez/claude-em (~95) | ★`.claude/skills/one-on-one` | **Best 1:1 prep skill.** Asks the manager 3 clarifying questions, reads the situation, then gives key questions, things to say, risks, if-then responses and an opening line. |
| 13 | simota/agent-skills (~98), NickCrew/Claude-Cortex (~66), paulip114/sre-practice-skills (~65) | `beacon`, `siege`, `magi` (risk), `sre-on-call-and-toil` | Toil and on-call |
| 14 | Happy-Technologies-LLC/happy-platform-skills (~41) | ★`skills/itsm/incident-triage` | **ServiceNow service-desk triage**: 5-level impact × urgency priority matrix, keyword-to-category mapping, assignment groups |
| Long tail (<40★) | lionelsimai/claude-skills-collection (`project-charter`, `one-on-one-template`), Owl-Listener/design-leadership-skills (`people-management/one-on-one`), stevenchouai/manage-up, camilooscargbaptista/cto-toolkit (`one-on-one`, `sprint-planning`), skills-on-ai (`project-charter`, `agile-charter`), marcbara/project-management-skills, curiositech/windags-skills (`interview-loop-strategist`), kryptophonik/SRE-Skills (`sre-toil-review`), caiaffa / paruff/fawkes / somnio (`dora-metrics`), clawic/skills (`cio`, `coo`) | | Niche |

**Gaps (no strong public skill found):** CAB meeting facilitation, ITIL problem management and known-error database (KEDB), knowledge management (KCS), SAFe PI planning, formal performance-review writing, ISO/IEC 20000 audit preparation. These are good candidates to write yourself.

**Starter set for a Claude "IT department" manager layer:** knowledge-work-plugins `operations` + `engineering`, wshobson `incident-response` + `slo-implementation`, alirezarezvani `senior-pm` + `scrum-master` + `vendor-management` + `incident-commander`, jcesarperez `one-on-one`, Happy-Technologies `incident-triage`.

---

## 2. Framework digests (สรุปกรอบแนวคิด)

### ITIL 4 (ระบบบริหารบริการ IT)
- **Core model:** Service Value System = guiding principles + governance + service value chain (plan, improve, engage, design & transition, obtain/build, deliver & support) + practices + continual improvement. **Four dimensions:** organisations & people; information & technology; partners & suppliers; value streams & processes.
- **7 guiding principles:** focus on value; start where you are; progress iteratively with feedback; collaborate and promote visibility; think and work holistically; keep it simple and practical; optimise and automate.
- **Incident management:** restore normal service as fast as possible. Priority = impact × urgency. Use swarming for complex incidents and a separate major-incident procedure. Measure MTTR, first-contact resolution and reopen rate.
- **Problem management:** three phases. (1) Identification, from trends and major incidents. (2) Control: root-cause analysis, then a **known error** recorded with its **workaround** in the KEDB. (3) Error control: permanent fix, usually through a change. Incident = symptom; problem = cause.
- **Change enablement:** three change types. **Standard:** pre-approved, low risk, scripted. **Normal:** assessed by a change authority, which in a large organisation is the CAB, or a peer review for low risk. **Emergency:** expedited, through an ECAB. ITIL 4 pushes to decentralise approval and automate it in the pipeline. Key artefacts: change schedule and forward schedule of change (FSC), success rate, failed-change rate.
- **Service request management:** routine pre-defined requests (access, hardware, information), fulfilled through a catalogue with standard workflows. Not incidents; aim to automate them.
- **Service level management (SLM):** agree SLAs; use OLAs (internal teams) and underpinning contracts (vendors) to back them. Measure with experience-based metrics as well as availability. Watch for the "watermelon SLA": green on the report, red for the user.
- **Knowledge management:** the right information to the right people at the right time. Pair with KCS: capture, structure, reuse, improve. Use the knowledge base for self-service deflection.
- **Service desk:** single point of contact, omnichannel, empathy plus triage. Escalate between tiers L0 (self-service) → L1 → L2 → L3/vendor.
- *Note:* PeopleCert has announced **ITIL (Version 5)**, focused on "digital product & service management". ITIL 4 practices remain the working baseline. Check the current certification path before you study.

### Google SRE
- **SLI / SLO / SLA:** SLI = a measured ratio of good events to valid events. SLO = the internal target over a window (e.g. 99.9% over 28 days). SLA = the contract with penalties, always looser than the SLO.
- **Error budget** = 1 − SLO. At 99.9%: 43.2 min per 30 days. Budget remaining → ship. Budget exhausted → freeze features and do reliability work. The policy must be agreed in writing by product, development and SRE.
- **Burn-rate alerting:** alert on how fast the budget is being consumed, using multiple windows. Typical pairs: 14.4× over 1h/5m pages; 6× over 6h/30m pages; 1× over 3d tickets.
- **Postmortem:** blameless. Write one for user-visible downtime, data loss, on-call intervention, resolution time over threshold, or a monitoring failure. Sections from the SRE book template: Summary, Impact, Root causes, Trigger, Resolution, Detection, Action items, Lessons (went well / went wrong / **where we got lucky**), Timeline.
- **Toil:** manual, repetitive, automatable, tactical, no lasting value, grows linearly with the service. Cap it at **≤50%** of SRE time and track it every quarter.
- **On-call:** at most ~25% of time on-call; about 2 incidents per 12-hour shift is sustainable; compensate on-call time; hold a ~30-min handoff overlap.
- **Incident roles** (IMAG/ICS, PagerDuty): Incident Commander, Ops/Tech lead, Comms lead, Scribe.

### DORA metrics
- **4 keys:** Deployment frequency, Lead time for changes (commit to production), Change failure rate, Time to restore. The latest reports rename the last one **Failed deployment recovery time**.
- Recent reports group them as **throughput** (deploy frequency, lead time, recovery time) and **instability** (change fail rate, plus a newer **rework rate**). Reliability, measured against your SLOs, is often tracked as a fifth metric.
- Elite benchmark: on-demand deploys, lead time under a day, recovery under an hour, change fail rate around 5% or less. Thresholds shift with each yearly report, so check the current one.
- Use the metrics for team improvement. Never use them to rank individuals.

### PMBOK 7 (PMI)
- Moved from processes (the old 10 knowledge areas, 49 processes) to principles.
- **12 principles:** stewardship, team, stakeholders, value, systems thinking, leadership, tailoring, quality, complexity, risk, adaptability & resilience, change.
- **8 performance domains:** stakeholders, team, development approach & life cycle, planning, project work, delivery, measurement, uncertainty.
- Tailor the approach: predictive, adaptive or hybrid.
- *PMBOK 8 (released ~late 2025) consolidates these. Check which edition your PMP exam uses.*

### PRINCE2 (7th edition, 2023)
- **7 principles:** continued business justification; learn from experience; defined roles, responsibilities and relationships; manage by stages; manage by exception (tolerances on time, cost, scope, quality, risk, benefits, sustainability); focus on products; tailor to the environment.
- **7 practices:** business case, organising, plans, quality, risk, issues, progress.
- **7 processes:** starting up, directing, initiating, controlling a stage, managing product delivery, managing a stage boundary, closing.
- **Project board:** Executive, Senior User, Senior Supplier.
- **"People"** is now an explicit element.

### Scrum, Kanban and SAFe
- **Scrum (2020 Guide):**
  - 3 accountabilities: Product Owner, Scrum Master, Developers.
  - 5 events: Sprint (≤1 month), Sprint Planning, Daily Scrum (15 min), Sprint Review, Retrospective.
  - 3 artefacts, each with a commitment: Product Backlog → Product Goal; Sprint Backlog → Sprint Goal; Increment → Definition of Done.
- **Kanban:** visualise the work, limit WIP, manage flow, make policies explicit, use feedback loops. Metrics: cycle time, throughput, WIP, work-item age. Kanban suits ops and service-desk teams better than Scrum.
- **SAFe 6:**
  - Agile Release Train of 50–125 people, delivering in Program Increments (PI) of 8–12 weeks.
  - **PI Planning:** 2 days, produces PI objectives and a dependency board.
  - Roles: RTE, Product Management, System Architect; Lean Portfolio Management with epics and guardrails.
  - Prioritise with **WSJF** = Cost of Delay ÷ Job Size.

### RACI
- **R**esponsible (does the work), **A**ccountable (exactly one per task, signs off), **C**onsulted (two-way), **I**nformed (one-way).
- Rules: exactly one A per row; avoid columns full of R; every row needs at least one R.

### ISO/IEC 20000-1:2018
- Certifiable service-management-system standard, aligned to ITIL and structured like ISO 9001/27001 (Annex SL).
- Clauses 4–10: context, leadership, planning, support, **operation** (clause 8: service portfolio and catalogue, SLM, supplier, budgeting, capacity, change, release & deployment, incident, request, problem, availability, continuity, information security), performance evaluation (internal audit, management review), improvement.
- Audits want evidence: records, KPIs, management-review minutes, corrective actions.

---

## 3. Templates (แม่แบบพร้อมใช้)

### T1. Incident report (รายงานเหตุขัดข้อง): live updates during an incident
```
INCIDENT #[ID] — [ชื่อเหตุการณ์ / Title]
Severity: SEV1/2/3/4 | Priority (Impact×Urgency): P1–P5 | Status: Investigating / Identified / Monitoring / Resolved
Incident Commander: __  Comms: __  Scribe: __  Tech lead: __
เริ่มเมื่อ (Start): __  ตรวจพบ (Detected): __  ประกาศ (Declared): __  แก้ไขแล้ว (Resolved): __
ผลกระทบ (Impact): ระบบ/บริการ __ | ผู้ใช้ที่ได้รับผลกระทบ __ (จำนวน/กลุ่ม) | ธุรกิจ __
สถานะปัจจุบัน (Current status): สิ่งที่รู้ตอนนี้ — facts only, no speculation
สิ่งที่ทำไปแล้ว (Actions taken): - __
ขั้นตอนถัดไป (Next steps + ETA): - __
Workaround สำหรับผู้ใช้: __
อัปเดตครั้งถัดไป (Next update at): __   (SEV1 every 15–30 min; SEV2 every 1 hr)
Timeline: | เวลา | เหตุการณ์ | ผู้ดำเนินการ |
```
Severity guide: SEV1 = service down for everyone, all hands now; SEV2 = major feature degraded, respond within 15 min; SEV3 = minor issue, within 1 hr; SEV4 = cosmetic, next business day.

### T2. Blameless postmortem (ทบทวนหลังเหตุการณ์ แบบไม่กล่าวโทษ)
Hold the review meeting within 5 business days. Draft the document on day 1–2 and track the action items afterwards.
```
POSTMORTEM: [Title] | Incident #__ | วันที่ __ | ระยะเวลา __ | SEV__ | ผู้เขียน __ | สถานะ Draft/Reviewed/Final
1. สรุป (Summary) — 2–3 ประโยค ภาษาที่ผู้บริหารเข้าใจ
2. ผลกระทบ (Impact) — ตัวเลขชัดเจน: เวลาที่อยู่ใน SEV1/2, ผู้ใช้/บัญชี, ธุรกรรมล้มเหลว, error budget ที่ใช้ไป %, ticket ที่เข้ามา
3. ผู้ตอบสนอง (Responders) — IC, scribe, others
4. ตัวกระตุ้น (Trigger) และ สาเหตุ/ปัจจัยร่วม (Root cause & contributing factors) — "เงื่อนไขอะไรที่ทำให้เกิดได้" not "ใครทำ"
5. การตรวจจับ (Detection) — ตรวจพบอย่างไร ช้า/เร็วแค่ไหน (TTD)
6. การแก้ไข (Resolution) — ชั่วคราว vs ถาวร
7. 5 Whys (ทำไม 5 ชั้น) — each "why" with evidence
8. อะไรทำได้ดี / อะไรไม่ดี / โชคช่วยตรงไหน (Went well / Went wrong / Where we got lucky)
9. Timeline (UTC/ICT) | เวลา | เหตุการณ์ | ลิงก์หลักฐาน |
10. Action items | # | งาน | ประเภท Prevent/Detect/Mitigate/Process | Owner | Priority P0–P2 | Due | Ticket |
11. การสื่อสาร (Messaging) — internal email + external/status-page text (genuine apology)
12. บทเรียน (Lessons learned)
```
Language rules: name systems and conditions, not people; every action has one owner and a ticket; review patterns across incidents every quarter.

### T3. Change request / CAB (คำขอเปลี่ยนแปลง)
```
CHANGE #[ID] — [Title]  | ผู้ขอ __ | วันที่ __ | ประเภท: Standard / Normal / Emergency
Priority: __ | Status: Draft → Submitted → Assessed → Approved/Rejected → Scheduled → Implemented → Reviewed/Closed
1. รายละเอียดการเปลี่ยนแปลง (What & why) + เหตุผลทางธุรกิจ (Business justification)
2. CI/ระบบที่เกี่ยวข้อง (Affected CIs/services) + dependencies
3. การวิเคราะห์ผลกระทบ (Impact): ผู้ใช้ / ระบบ / กระบวนการ / ค่าใช้จ่าย — H/M/L + รายละเอียด (e.g. "200 users in billing", not "everyone")
4. การประเมินความเสี่ยง (Risk): | ความเสี่ยง | โอกาส | ผลกระทบ | การลดความเสี่ยง | → Risk score
5. แผนการดำเนินการ (Implementation plan): steps, owner, start/end, maintenance window, downtime expected?
6. แผนทดสอบ (Test plan) — pre- and post-implementation verification
7. แผนย้อนกลับ (Rollback/backout plan): trigger condition, steps, time needed, verification
8. แผนสื่อสาร (Communication): | กลุ่ม | ข้อความ | ช่องทาง | เวลา |
9. ตรวจสอบปฏิทิน (Change calendar check): conflicts, freeze periods, error budget status
10. การอนุมัติ (Approvals): | ผู้อนุมัติ | บทบาท | สถานะ | วันที่ |
11. ทบทวนหลังเปลี่ยนแปลง (PIR): success / failed / rolled back; incidents caused?
```
**CAB agenda (60 min, weekly):** (1) Review last week's changes: success rate, failed changes, incidents caused by changes. (2) Emergency changes since the last meeting (ratify them). (3) New normal changes, ordered by risk score: present, ask questions, then approve, reject or defer. (4) Forward schedule of change and freeze windows. (5) Candidates to move to the pre-approved Standard list. (6) Action items.

### T4. SLA/SLO sheet (เอกสารระดับบริการ)
```
บริการ (Service): __ | เจ้าของบริการ (Service owner): __ | ลูกค้า/ผู้ใช้: __ | เวลาให้บริการ (Hours): 24×7 / 8×5 ICT
| SLI (ตัวชี้วัด) | นิยาม good/valid | SLO (เป้าภายใน) | หน้าต่าง | SLA (สัญญา) | Error budget |
| Availability | non-5xx / all requests | 99.9% | 28d rolling | 99.5% | 40.3 min/28d |
| Latency | requests <300 ms / all | 99% | 28d | 95% <1 s | 1% of requests |
| Freshness/Correctness | ... | | | | |
เวลาตอบสนอง/แก้ไขของ Service desk:
| Priority | Response | Resolution target | Update cadence | Escalation |
| P1 | 15 min | 4 h | 30 min | Duty manager → IT Manager → CIO |
| P2 | 30 min | 8 h | 2 h | |
| P3 | 4 h | 3 business days | daily | |
| P4 | 1 business day | 10 business days | — | |
นโยบาย Error budget: >50% remaining = normal; <50% = review risky changes; <10% = freeze non-critical changes; 0% = feature freeze, reliability work only
Burn-rate alerts: 14.4× (1h/5m) page; 6× (6h/30m) page; 1× (3d) ticket
OLA/UC ที่รองรับ: __ (internal teams / vendors)
ข้อยกเว้น (Exclusions): planned maintenance with ≥5 days' notice, force majeure, customer-caused
บทลงโทษ/เครดิต (Service credits): __ | รอบทบทวน (Review): monthly report, quarterly SLO review
```
Availability reference: 99% ≈ 7.2 h/month; 99.9% ≈ 43 min; 99.95% ≈ 22 min; 99.99% ≈ 4.3 min.

### T5. Project charter (กฎบัตรโครงการ)
```
ชื่อโครงการ __ | รหัส __ | Sponsor (ผู้สนับสนุน) __ | Project Manager __ | วันที่ __ | Version __
1. ที่มาและปัญหา (Background / problem statement)
2. วัตถุประสงค์ SMART (Objectives) + ตัวชี้วัดความสำเร็จ (Success criteria/KPIs) + benefits & who measures them
3. ขอบเขต (Scope) — In scope / Out of scope
4. ส่งมอบหลัก (Key deliverables)
5. Milestones & timeline (ไตรมาส/วันที่)
6. งบประมาณ (Budget) CAPEX/OPEX + contingency %; tolerances (±time/±cost) for escalation
7. ผู้มีส่วนได้ส่วนเสีย (Stakeholders) + RACI สรุป
8. โครงสร้างทีม/คณะกรรมการ (Governance: steering committee, cadence, decision rights)
9. สมมติฐาน (Assumptions) / ข้อจำกัด (Constraints) / Dependencies
10. ความเสี่ยงสำคัญเบื้องต้น (Top risks) — link to the risk register
11. แนวทางการพัฒนา (Approach): predictive / agile / hybrid
12. การอนุมัติ (Sign-off): Sponsor, PM, key stakeholders
```

### T6. Status report (รายงานความคืบหน้า): weekly or monthly
```
รายงานสถานะ: [โครงการ/ทีม] — [ช่วงเวลา] | ผู้รายงาน __
สถานะรวม: 🟢 ตามแผน / 🟡 มีความเสี่ยง / 🔴 ล่าช้า  (Scope __ Schedule __ Budget __ Quality __)
สรุปผู้บริหาร (3 บรรทัด): what's on track, what needs attention, key win
ตัวชี้วัด: | KPI | เป้า | จริง | แนวโน้ม | สถานะ |
ผลงานรอบนี้ (Accomplishments): -
กำลังดำเนินการ: | งาน | owner | สถานะ | ETA |
ความเสี่ยง/ปัญหา: | เรื่อง | ผลกระทบ | การจัดการ | owner |
ต้องการการตัดสินใจ (Decisions needed): | เรื่อง | บริบท | deadline | ข้อเสนอแนะ |
แผนรอบถัดไป: 1. 2. 3.
```
Tips: lead with the headline; report red early; every decision request comes with your recommendation. For exec reports use Situation → Impact → Resolution.

### T7. Risk register (ทะเบียนความเสี่ยง)
```
| ID | ความเสี่ยง (If [cause], then [event], resulting in [impact]) | หมวด Ops/Fin/Compliance/Security/Strategic/Reputation | โอกาส 1–5 | ผลกระทบ 1–5 | คะแนน (L×I) | ระดับ | กลยุทธ์ Avoid/Reduce/Transfer/Accept (+Exploit for opportunities) | แผนลดความเสี่ยง | Trigger/สัญญาณเตือน | Owner | Due | สถานะ Open/Mitigating/Accepted/Closed | Residual score | อัปเดตล่าสุด |
```
Scoring: 1–4 Low, 5–9 Medium, 10–16 High, 20–25 Critical. Review High and above weekly and the full register monthly. Every Accept decision needs a named approver.

### T8. Weekly ops review agenda (ประชุมทบทวนงานปฏิบัติการประจำสัปดาห์): 45–60 min
1. **Wins and shout-outs** (3 min)
2. **Service health vs SLO:** error-budget burn per service, availability, latency (10 min)
3. **Incidents:** count by SEV, MTTA/MTTR, any SEV1/2 summary, postmortems due or overdue, action-item burndown (10 min)
4. **Problems:** top recurring incidents, new known errors and workarounds, RCA status (5 min)
5. **Changes:** last week's success rate and failed changes, emergency changes, next week's schedule and freezes (5 min)
6. **Service desk:** ticket volume and backlog age, SLA breaches, first-contact resolution, CSAT, top 5 categories → knowledge articles or automation (5 min)
7. **Capacity and cost:** hotspots at >70–80% utilisation, cloud spend vs budget (5 min)
8. **On-call health:** pages per shift, after-hours pages, toil hours, noisy alerts to fix (5 min)
9. **Risks, vendors, escalations** (5 min)
10. **Action items recap:** owner and date for each (2 min)

### T9. Team 1:1 agenda (ประชุมตัวต่อตัวกับลูกทีม): 30 min, weekly or biweekly
The agenda belongs to the report: they fill it in first.
1. **เรื่องของคุณ (Their topics first):** whatever is on their mind (10–15 min)
2. **ความเป็นอยู่/ภาระงาน (Wellbeing and load):** energy, workload 1–5, blockers I can remove
3. **งาน (Work):** progress against goals and priorities, decisions they need from me
4. **ฟีดแบ็ก 2 ทาง (Two-way feedback):** one specific piece from me (situation, behaviour, impact); "What should I start/stop doing?"
5. **การเติบโต (Growth), monthly:** career goals, a skill to stretch, a project opportunity, evidence against the career framework
6. **สรุป (Wrap-up):** agreed actions, owner, date, written in the shared 1:1 doc

Manager prep, from the claude-em skill: what is the goal of this 1:1? Which facts are observed and which are assumed? Pick 3–5 sharp questions, prepare an opening line and plan responses for the likely reactions. Never cancel a 1:1; reschedule it.

---

## 4. Manager's checklist (เช็กลิสต์ผู้จัดการ IT)

**Daily (≤15 min)**
- [ ] Open P1/P2 incidents and SLA-breach risk
- [ ] Today's changes and the on-call handoff note
- [ ] Unblock the team

**Weekly**
- [ ] Run the ops review (T8) and CAB (T3)
- [ ] All 1:1s held (T9)
- [ ] Send the status report (T6) to your manager and stakeholders
- [ ] Review High risks (T7)
- [ ] Check postmortem action items for overdue ones and chase owners
- [ ] Error-budget status → adjust release or freeze decisions
- [ ] Service-desk backlog older than 7 days
- [ ] Recognise one person publicly

**Monthly**
- [ ] SLA/SLO report per service (watch for watermelon SLAs) → service review with business owners
- [ ] DORA metrics trend; change success rate
- [ ] Problem review: top 10 recurring incidents and the KEDB
- [ ] Capacity and cost review, forecast vs actual budget
- [ ] Vendor scorecards: SLA compliance, credits due, upcoming renewals (90-day lookahead)
- [ ] Full risk-register review
- [ ] Knowledge-base gaps from ticket categories
- [ ] Toil and on-call load per person
- [ ] Skip-levels or team health check
- [ ] Training budget and certifications

**Quarterly / yearly**
- [ ] OKRs, roadmap and portfolio reprioritisation (WSJF)
- [ ] Headcount and capacity plan
- [ ] SLO targets review
- [ ] DR/BCP test
- [ ] Access review
- [ ] Contract renewals
- [ ] Performance and calibration reviews
- [ ] Postmortem pattern analysis
- [ ] Internal audit / management review (ISO 20000 evidence)
- [ ] Yearly: budget cycle

---

## 5. URLs that failed

**Blocked by the network proxy (403 on connect):**
- `skills.sh` (both the API and search pages), so there are no install counts and ranking is by stars
- `sre.google/sre-book/example-postmortem/`, `sre.google/workbook/error-budget-policy/`, `sre.google/sre-book/eliminating-toil/`
- `dora.dev/guides/dora-metrics-four-keys/`
- `response.pagerduty.com`
- `axelos.com` (ITIL)
- `pmi.org/standards/pmbok`
- `scrumguides.org`
- `framework.scaledagile.com`
- `iso.org/standard/70636.html`

**Blocked by session scope (403):** the GitHub `repos/*` metadata API for every repository. Star counts came from `search/repositories` instead.

**Stub only:** `majiayu000/claude-skill-registry/.../itil-expert/SKILL.md` is now just a pointer to an archive repo.

**What worked:** raw.githubusercontent.com for every SKILL.md listed above, the PagerDuty postmortem template, and the dastergon copy of the Google SRE-book template.
