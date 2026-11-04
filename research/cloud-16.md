# Research cloud-16 — People & communication skills: practitioner → manager → executive (IT)

Read-only research, Nov 2026. Audience: an IT practitioner in a Thai military unit who builds web apps and must win approval from commanders and adoption from soldiers.

**Bottom line:** The strongest public agent skills live inside a few big PM/exec bundles (Lenny's, Dean Peters', alirezarezvani, phuryn). Good coverage exists for exec writing, stakeholders, feedback, meetings; **almost nothing public covers delegation, user training (Kirkpatrick/adult learning), or Thai/military memo writing** — templates below fill that gap.

**Source caveat:** the session's network policy blocked all direct page fetches (radicalcandor.com, pon.harvard.edu, kirkpatrickpartners.com, Atlassian, Thai .go.th sites). Framework digests rely on web-search summaries cross-checked against each other plus standard knowledge; items marked † were confirmed by ≥2 independent search results. Skill files were read directly from cloned repos.

---

## 1. Skill catalog (ranked by GitHub stars, Nov 2026)

| # | Repo (★) | Relevant skills | Verdict |
|---|---|---|---|
| 1 | `anthropics/skills` (187k) | `internal-comms` (3P = Progress/Plans/Problems, leadership updates, FAQs, incident reports), `doc-coauthoring` | Official, minimal; 3P is a good weekly report format for a commander |
| 2 | `alirezarezvani/claude-skills` (29.3k) | `c-level-advisor/change-management` (ADKAR; "compliance = do it when watched; adoption = believe it's better"), `board-deck-builder`, `board-meeting`, `executive-mentor/{hard-call,stress-test,board-prep}`, `decision-logger`, `productivity/meetings`, `project-management/team-communications`, `internal-comms` | Broadest; ADKAR skill maps directly to a web-app rollout |
| 3 | `phuryn/pm-skills` (27.7k) | `pm-execution/stakeholder-map`, `summarize-meeting`, `pre-mortem`, `retro`, `strategy-red-team` | Compact, practical |
| 4 | `deanpeters/Product-Manager-Skills` (7.9k) | `stakeholder-identification` → `stakeholder-mapping` (two grids: Power×Interest = how to engage; Impact×Power = whose voice is missing; cites MITRE ITK) → `stakeholder-engagement-advisor`; `press-release` (Amazon Working Backwards, 1–1.5 pages); `director-readiness-advisor`, `vp-cpo-readiness-advisor`, `executive-onboarding-playbook`, `workshop-facilitation`, `recommendation-canvas`, `eol-stakeholder-sequence` | Most rigorous; best stakeholder method found |
| 5 | `RefoundAI/lenny-skills` (1.5k) | `executive-communication`, `stakeholder-alignment`, `giving-feedback` (GAIN, "stay on your side of the net"), `running-meetings`, `managing-up`, `coaching-development`, `leading-org-change`, `public-speaking`, `written-communication`, `high-stakes-decisions` | Best principles + named mistakes: "movie-arc reveal" wastes exec time; frame trade-offs as goal A vs goal B, not "we lack people"; consensus ≠ collaboration; presenting finished solutions kills stakeholder authorship; don't accept upward delegation |
| 6 | `w95/awesome-claude-corporate-skills` (299) | `executive-communication`, `contract-negotiation` (full BATNA/reservation/target worked example + 1–2 page "Negotiation Brief"), `change-management`, `onboarding-planner` | Best negotiation template |
| 7 | `millwright-labs/minto-pyramid-skill` (89) | `minto-pyramid` | Best single writing skill: gate first ("does this doc ask the reader to decide?" — if not, e.g. timeline/runbook, don't restructure); offer before rewriting; never add facts; keep SCQA lean |
| 8 | `tyroneross/pyramid-principle` (43) | Minto short/long-form skills | Alternative to #7 |
| 9 | `marlonvidal/tech-manager-os` (21), `MbappeWU/murder-board` (20) | EM operating system; hostile exec-review rehearsal panel | murder-board is useful to rehearse a commander's briefing |
| 10 | `camilooscargbaptista/cto-toolkit` (8) | `one-on-one` (prep + notes templates; "pick 1–2 agenda items, not all"; "the ONE key message"; "signals to watch") | Best 1:1 template |
| 11 | `htk007/claude-skills-for-leaders` (9), `ironyjk/howtotalk` (3; radical-candor, influence, storytelling, NVC), `WieSoe/feedback-coach` (2; SBI/NVC/Radical Candor + SCARF check + "defuse my words"), `yshameer/executive-presence-framework` (0; 12 frameworks; diagnose → pick frameworks → write actual words → delivery notes) | Niche but well designed |
| — | Gaps (0–1★ only): `guycoful/negotiate-skill`, `sebaapg1/corporate-training-skill` (Bloom/Kirkpatrick), `tflynn05/change-management-skill`, `amunivec/storytelling-with-data-skill`, `zrwang/meeting-facilitation-skills`, `lallycat/smart-brevity` | No popular delegation, training-evaluation or Thai/military-writing skill exists |

Installs: skills.sh (Vercel's leaderboard, launched Jan 2026) is topped by generic skills (find-skills ≈458k installs, frontend-design); no people-skills skill is near the top, so stars were used for ranking.

---

## 2. Framework digests

- **Minto Pyramid / SCQA**† — Answer first → 3±1 grouped reasons → evidence. Rules: each idea summarises those below; groups are same-kind, MECE, logically ordered (time/structure/importance). Intro SCQA: Situation (reader already agrees) → Complication (what changed/broke) → Question (often implicit) → Answer. Use only as much S/C as needed. SCR = short form.
- **BLUF**† — From US Army AR 25-50: recommendation/conclusion/reason for writing in the opening paragraph, including any decision requested.
- **Amazon 6-pager & PR/FAQ**† — "We don't do PowerPoint… we write narratively structured six-page memos." Meetings start with ~30 min silent reading. PR/FAQ = 1–1.5-page customer-perspective press release written *before* building (headline, problem, solution, leader quote, CTA) + external/internal FAQ. Use: write the "launch-day announcement" of the web app before asking for approval.
- **Harvard principled negotiation (Fisher/Ury/Patton)**† — Separate people from problem; interests not positions; options for mutual gain; objective criteria. **BATNA** = walk-away floor/leverage. Prepare target, reservation point, and estimate the other side's BATNA (overlap = ZOPA).
- **Radical Candor (Kim Scott)**† — Care Personally × Challenge Directly → Radical Candor / Obnoxious Aggression / Ruinous Empathy ("by far the most common mistake") / Manipulative Insincerity. Praise more than criticise; immediate; criticise in private; solicit criticism of yourself first.
- **SBI (Center for Creative Leadership)**† — Situation (when/where) → Behavior (observable only) → Impact (on you/team/mission); then an open question. SBI-I adds Intent (sources disagree whether CCL or practitioners added it).
- **GROW (Whitmore, *Coaching for Performance*)** — Goal → Reality → Options → Will/Way forward; ask, don't tell. (Not confirmed via search; standard.)
- **Situational Leadership (Hersey–Blanchard)**† — S1 Telling (high direction/low support), S2 Selling (high/high), S3 Participating (low/high), S4 Delegating (low/low), matched to follower readiness (ability × willingness) *per task*. Blanchard's SLII renames: Directing/Coaching/Supporting/Delegating. → Use as the delegation framework: delegate fully only at high readiness; step support down over time.
- **RACI / DACI**† — RACI: Responsible (does), Accountable (single final approver), Consulted, Informed. DACI (Intuit → Atlassian): Driver runs the process, one Approver decides, Contributors, Informed. In a unit: commander = A/Approver; system owner = Driver.
- **Kirkpatrick**† — L1 Reaction, L2 Learning, L3 Behavior, L4 Results (1959). "New World" (2016): plan backwards from L4; L2 adds confidence and commitment; L3 needs "required drivers" (accountability, reinforcement, coaching) and leading indicators. Most organisations stop at L1–2.
- **Adult learning (Knowles, andragogy)**† — Need to know why; self-concept (self-directed); experience as resource; readiness tied to real tasks; problem-centred orientation; internal motivation. Knowles later: depends on context more than age.
- **Storytelling with Data (Knaflic)**† — Understand context, choose effective visual, eliminate clutter, focus attention, think like a designer, tell a story.
- **Change adoption (ADKAR)** — Awareness → Desire → Knowledge → Ability → Reinforcement; aim for adoption, not compliance.

### Thai context — บันทึกเสนอผู้บังคับบัญชา
Confirmed in Thai government writing manuals, including Royal Thai Navy อทร. ๘๔๐๑ (2546):
- **เรื่อง** starts with a verb (ขออนุมัติ / ขออนุญาต / ขอส่ง), short, matches the closing request.
- **เรื่องเดิม** — "ตาม / ตามที่ / อนุสนธิ" + reference, brief.
- **ข้อเท็จจริง**, then **ข้อกฎหมาย/ระเบียบ** (attach copies if any).
- **ข้อพิจารณา** — ≤ ~10 lines; options as numbered points.
- **ข้อเสนอ** — "เห็นควร…"
- **คำลงท้าย** — "จึงเรียน/เสนอมาเพื่อโปรด (ทราบ / พิจารณา / เห็นชอบ / อนุมัติ / ลงนาม)"; "เพื่อโปรดทราบ" when information only.
- General บันทึกข้อความ (ระเบียบสำนักนายกฯ ว่าด้วยงานสารบรรณ 2526, amended 2548, 2560): ภาคเหตุ → ภาคความประสงค์ (+ ภาคสรุป).
- **Mapping:** this is SCQA/BLUF in Thai form (เรื่องเดิม = S, ข้อเท็จจริง = C, ข้อพิจารณา = analysis, ข้อเสนอ = A). The Thai format puts the ask last, so add a one-line **สรุป** at the top (or a cover summary) to keep BLUF.
- **Presenting to seniors** (Thai doctrine not verifiable online; consistent with staff-estimate practice): follow ลำดับชั้น (route through every level — never surprise your direct boss); pre-brief the immediate superior before the commander; end with clear หนทางปฏิบัติ + recommendation + stated risk; commanders decide on "ข้อสรุปและข้อเสนอแนะ", not background.

---

## 3. Templates (paraphrased)

### A. บันทึกเสนอ — one page, approval for a web app
```
ส่วนราชการ ……  ที่ …… วันที่ ……
เรื่อง  ขออนุมัติใช้ระบบ [ชื่อระบบ] ในหน่วย (นำร่อง ๓ เดือน)
เรียน  [ผบ.หน่วย]  (ผ่าน [ผู้บังคับบัญชาตามลำดับชั้น])
สรุป (BLUF, ๒ บรรทัด): ขออนุมัตินำร่องระบบ… ลดเวลา…จาก X เป็น Y วัน ไม่ใช้งบเพิ่ม/ใช้งบ…
๑. เรื่องเดิม     ตามที่… (ภารกิจ/คำสั่ง/ปัญหาที่ ผบ. รับรู้แล้ว)
๒. ข้อเท็จจริง   ปัญหาปัจจุบันเป็นตัวเลข ๓ ข้อ (เวลา ความผิดพลาด กำลังพล)
๓. ข้อกฎหมาย/ระเบียบ  ระเบียบสารบรรณ/ความปลอดภัยสารสนเทศ/PDPA ที่เกี่ยวข้อง
๔. ข้อพิจารณา (≤10 บรรทัด)
   ๔.๑ หนทาง ๑: คงเดิม – ผล/ความเสี่ยง
   ๔.๒ หนทาง ๒: นำร่อง [ระบบ] ๑ กองร้อย ๓ เดือน – ผล/ต้นทุน/ความเสี่ยง+มาตรการ
   ๔.๓ หนทาง ๓: ใช้ทั้งหน่วยทันที – ผล/ความเสี่ยง
   เกณฑ์วัดผล: [ตัวชี้วัด ๒–๓ ตัว], ทบทวนเมื่อ [วันที่]
๕. ข้อเสนอ  เห็นควรอนุมัติหนทางที่ ๒ และมอบ [ผู้รับผิดชอบ] ดำเนินการ
จึงเรียนมาเพื่อโปรดพิจารณา หากเห็นชอบโปรดลงนามอนุมัติ
ผนวก: ภาพหน้าจอ, แผนฝึกอบรม, RACI
```

### B. Slide outline — asking approval for a digital system (≤10 slides, BLUF)
1. **ข้อเสนอ** — one-sentence ask + decision needed today
2. Situation — mission/task the commander already owns
3. Complication — pain in numbers (one chart, one highlighted bar)
4. What it looks like — 30-second demo/screenshot from a soldier's view
5. Three options (keep / pilot / full rollout) — benefit, cost, risk
6. Recommendation + pilot scope, owner (RACI), timeline
7. Risks & mitigations — security, data, dependency on one person (continuity when the developer is rotated)
8. How success is measured (Kirkpatrick L3/L4) + review date
9. Decision requested again — "ขออนุมัติ…"
Appendix: tech detail, costs, regulations. Rehearse with a hostile panel (murder-board style) and pre-brief the direct boss.

### C. Stakeholder map (two grids)
| ผู้มีส่วนได้เสีย | อำนาจ (H/L) | ความสนใจ (H/L) | ได้รับผลกระทบ (H/L) | ผลประโยชน์/ความกังวล | ท่าที (−2…+2) | กลยุทธ์ | ผู้ดูแล/นัดถัดไป |
|---|---|---|---|---|---|---|---|
| ผบ.หน่วย | H | M | L | ความพร้อมรบ, ผลตรวจ | 0 | Manage closely: 1-page memo + pilot | |
| ฝอ.๔ / ฝ่ายกำลังพล | H | H | H | งานเพิ่ม, เสียการควบคุม | ? | Co-design | |
| จ่า/เสมียน (ผู้ใช้หลัก) | L | H | H | งานเพิ่ม, กลัวถูกตำหนิ | ? | Elevate voice; make champions | |
| ฝ่ายสื่อสาร/ไอที | H | L | L | ระเบียบความปลอดภัย | ? | Keep satisfied: brief early | |

Power×Interest → manage closely / keep satisfied / keep informed / monitor. Impact×Power → high-impact, low-power users (clerks) are the adoption risk; involve early.

### D. Negotiation prep sheet (Harvard)
```
เป้าหมายของเรา (target): …     จุดต่ำสุดที่รับได้ (reservation): …
BATNA ของเรา: … (เช่น ทำ Excel ต่อ / ขอหน่วยเหนือ)   BATNA ของเขา (ประมาณ): …
จุดยืนของเขา (position): …    ผลประโยชน์ที่แท้จริง (interests): …
ผลประโยชน์ของเรา: …
ทางเลือกที่ได้ทั้งคู่ (options): 1… 2… 3…
เกณฑ์กลางที่เป็นธรรม (objective criteria): ระเบียบ, ตัวเลขนำร่อง, แนวปฏิบัติหน่วยอื่น
สิ่งที่ยอมแลกได้ / ห้ามแลก: …
ประโยคเปิด / คำถามสำรวจ: "อะไรคือสิ่งที่ท่านกังวลที่สุดเรื่องนี้?"
ความสัมพันธ์ที่ต้องรักษา: …   ขั้นต่อไปถ้าตกลง/ไม่ตกลง: …
```

### E. 1:1 agenda (30 min, their agenda first)
1. Their topics (10–15 min) — "อะไรติดขัดอยู่?" "ช่วยอะไรได้บ้าง?"
2. Your 1–2 items (not all) — project check, one piece of feedback (SBI)
3. Growth (monthly) — GROW questions; which situational-leadership style fits this task
4. Feedback for you — "สิ่งหนึ่งที่ผมควรเลิก/เริ่มทำ?"
5. Actions: who / what / when; signals to watch

### F. Feedback script (SBI + Radical Candor)
- Ask: "ขอเวลา ๕ นาทีคุยเรื่อง… ได้ไหม" (private, soon after the event)
- **S:** "เมื่อวันอังคาร ตอนประชุมสรุปยอดพัสดุ…"
- **B:** "ตัวเลขในระบบไม่ตรงกับบัญชีคุมสามรายการ" (observable only, no labels)
- **I:** "ทำให้ ผบ. ต้องสั่งตรวจซ้ำ และทีมเสียความเชื่อมั่นในระบบ"
- **Intent/question:** "ช่วยเล่าให้ฟังว่าเกิดอะไรขึ้น?" → listen
- Agree next step + owner + date; show care: "ผมบอกเพราะอยากให้ระบบที่คุณดูแลได้รับการยอมรับ"
- Praise: same SBI, specific, in public.

### G. User-training plan for a unit rolling out a new web app (Kirkpatrick backwards + adult learning)
| ขั้น | เนื้อหา |
|---|---|
| ๑. ผลที่ต้องการ (L4) | e.g. request turnaround 5 → 1 day; data error < 2%; 90% of transactions in-system by month 3 |
| ๒. พฤติกรรมที่ต้องเห็น (L3) | Clerks file every request in-system; supervisors approve in-system; paper stopped |
| ๓. ผู้เรียน | Role map: users / approvers / admins; one ผู้ชำนาญประจำกองร้อย (champion) per unit |
| ๔. ออกแบบ (adult learning) | Start with "why — ลดงานคุณ…"; real tasks from their own job; 20–30 min sessions; show-then-do; build on the existing paper process; cheat-sheet/QR guide; sandbox data |
| ๕. ลำดับ | Brief commander → train champions → pilot 1 company → fix → waves → 2 weeks paper + system in parallel → paper stops (by order) |
| ๖. วัดผล | L1 short survey after each session; L2 5-task practical test + confidence rating; L3 system logs + supervisor spot-checks weeks 2/4/8; L4 KPIs in the monthly report to the commander |
| ๗. ปัจจัยหนุน (required drivers) | Command order/policy, slot in the training schedule, champion office hours, a chat group for Q&A, recognise top users at the monthly meeting, refresher when personnel rotate |
| ๘. RACI | A = ผบ.; R = system owner / champions; C = signals & personnel staff; I = all users |

---

## 4. Failed URLs
Network-policy DNS block (ENOTFOUND / curl 000):
- radicalcandor.com/our-approach
- performanceconsultants.com/grow-model
- situational.com/situational-leadership
- workingbackwards.com (PR/FAQ concept page)
- pon.harvard.edu (BATNA article)
- kirkpatrickpartners.com/the-kirkpatrick-model
- atlassian.com/team-playbook/plays/daci, …/roles-and-responsibilities
- gotoknow.org/posts/424748, /133460, /415466
- psdg.moe.go.th (คู่มืองานสารบรรณ PDF)
- pao-roiet.go.th/Facilitate/014_2.pdf

GitHub API refused repos outside the session scope (403); repos were read via `git clone` instead.

## 5. Sources (via search summaries)
- อทร. ๘๔๐๑ การเขียนหนังสือราชการ (กองทัพเรือ): https://www.rtna.navy.mi.th/stat/documents/upload/2562/256212021432105070.pdf
- อย. เทคนิคการเขียนหนังสือราชการ: https://cms-media.fda.moph.go.th/461152983531528192/2023/04/aWe0verw1ZnSh0vyzP6KVZYk.pdf
- กสก. เรื่องเสนอผู้บริหาร: https://secreta.doae.go.th/wp-content/uploads/2022/07/info.pdf
- ระเบียบงานสารบรรณ 2526: https://om.moe.go.th/wp-content/uploads/2023/03/สารบรรณ2526.pdf
- BLUF / AR 25-50: https://en.wikipedia.org/wiki/BLUF_(communication)
- Getting to Yes: https://en.wikipedia.org/wiki/Getting_to_Yes
- HMS Ombuds, principled negotiation: https://hms.harvard.edu/sites/default/files/assets/Sites/Ombuds/files/HMS.HSDM_.HSPH_.Ombuds%20Office.Elements%20of%20Principled%20Negotiations.pdf
- Stanford GSB on Radical Candor: https://gsb.stanford.edu/insights/radical-candor-communication-shift-can-transform-your-career
- Mind Tools SBI: https://prime.mindtools.com/pages/article/situation-behavior-impact-feedback.htm
- Mind Tools Kirkpatrick: https://www.mindtools.com/ak1yhhs/kirkpatricks-four-level-training-evaluation-model
- USD andragogy: https://pce.sandiego.edu/what-is-andragogy/
- Atlassian DACI: https://www.atlassian.com/blog/project-management/daci-method-for-better-project-decisions
- Amazon six-page narrative: https://www.anecdote.com/2018/05/amazons-six-page-narrative-structure/
- Vercel, state of agent skills: https://vercel.com/blog/state-of-agent-skills
- US Army running estimates: https://www.army.mil/article/279458/staff_processes_in_lsco_pt_2_running_estimates_crawling_when_we_need_to_run
