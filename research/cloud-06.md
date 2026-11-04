# Agent Skills Playbook: How Top Authors Write, Test and Chain Skills

Research report. Sources: anthropics/skills, obra/superpowers, mattpocock/skills,
addyosmani/agent-skills, vercel-labs/skills, agentskills/agentskills (spec repo), and the
live Anthropic / Claude Code skills docs. Read-only study; no evals were run.

**Where the sources disagree, and how I settled it:**
- **What the description says.** Anthropic and agentskills.io say a description should state
  *what* the skill does and *when* to use it. obra says *when* only, because an agent that
  reads a step summary in the description follows that summary and skips the body. Rule: name
  the domain and the outputs (nouns), plus when to use it, and never list the steps.
- **How pushy to be.** Anthropic's skill-creator says Claude tends to under-use skills, so
  descriptions should be "pushy". Its own `prompt-audit.md` says capital-letter boosters like
  "CRITICAL: MUST" now cause over-use. Rule: be broad about *which situations* count, at normal
  volume, with no capitals.
- **Prohibitions.** obra uses "never X" lists for discipline rules. mattpocock says banning a
  behaviour puts it in the agent's head and makes it more likely. obra's own wording tests show
  both are right, for different kinds of failure (rule C5).

---

# 1. The playbook (rules with examples)

## A. Description and trigger writing (the most important file content)

**A1. The description is the only thing loaded before the skill fires.** It has to carry all of
the "when should I use this?" information. Put "when to use" text in the description, not in
the body.

**A2. Formula:** the domain and its outputs (nouns), then "Use when..." with the different
situations that should trigger it, then a "Not for..." boundary when a sibling skill is close.
Write it in third person or as an instruction, never "I can...".
```yaml
# ❌ Too vague, and it lists the workflow
description: Helps with official forms. Gathers info, fills template, checks format, exports PDF.
# ✅
description: Government separation and pension paperwork produced as print-ready PDF/DOCX in the official format. Use when the user needs any such document drafted, filled or checked, even if they only paste a photo of the form or describe their situation in their own language. Not for general letters (use writing-letters).
```

**A3. Don't summarise the steps in the description.** In obra's test, a description that said
"code review between tasks" made the agent do one review instead of the two in the body.

**A4. Be broad about situations, not loud.** Use "even if they don't say X" or "even when it's
pasted inline". Measured result from addyosmani's evals: adding *"applies even when the code is
pasted inline"* took a review skill from 7/27 fires to 21/27, with 0 false fires. Skip
"CRITICAL / MUST / YOU ABSOLUTELY". Current models over-use skills whose descriptions shout.

**A5. One trigger per situation.** Synonyms for the same case count once. Don't keep adding the
exact phrasings of missed queries; name the broader kind of request instead.

**A6. Put the most important words first.** Claude Code cuts `description` + `when_to_use` at
**1,536 characters**. The whole skill list gets about **1% of the context window**, and when it
overflows, descriptions of rarely used skills are dropped. With a few dozen skills, aim for
**under 500 characters each** (obra's advice).

**A7. Decide who can start it:**
- Side effects or timing matter (deploy, publish, send): `disable-model-invocation: true`. Only
  the user can start it, it costs no context, and its description becomes a one-line note for
  the user.
- Background knowledge the user would never type as a command: `user-invocable: false`.
- When you have many user-only skills, add **one router skill** that lists them and when to use
  each (mattpocock's `ask-matt`).

**A8. Name rules:** max 64 characters, lowercase letters, digits and hyphens, no leading,
trailing or double hyphens, must match the folder name, and can't contain "claude" or
"anthropic". Names that say what you do work best (`filling-forms`, `condition-based-waiting`).
Avoid `helper`, `utils`, `docs`.

## B. File layout and length limits

```
skill-name/
├── SKILL.md        # required; body <500 lines / <5,000 tokens (target <500 words if often loaded)
├── references/     # loaded on demand; one level deep; TOC if >300 lines (Anthropic docs: >100 lines)
├── scripts/        # executed, not read (costs ~0 context); run via interpreter: `python3 scripts/x.py`
├── assets/         # templates, fonts, images used in OUTPUT
└── evals/evals.json  # test prompts + assertions (skill-creator schema)
```
- **B1. Three loading levels.** Name and description (~100 tokens) are always loaded. The body
  loads when the skill fires. Files load only when the body points to them.
- **B2. Every pointer says *when* to read the file.** "Read `references/api-errors.md` if the
  API returns non-200" works; "see references/" doesn't.
- **B3. Most important rules go near the top.** After compaction, Claude Code keeps only the
  first **5,000 tokens** of each skill used, with **25,000 tokens** shared across all of them.
- **B4. Split by situation.** Keep inline what every case needs. Push out what only some cases
  reach (e.g. `references/aws.md`, `gcp.md`). Don't use `@file` links, which force-load the
  file right away.
- **B5. Validator gotcha.** Claude Code-only fields (`disable-model-invocation`,
  `argument-hint`, `context: fork`, `paths`, `hooks`, `model`, `when_to_use`) fail
  skill-creator's `quick_validate.py` and the agentskills spec, which allow only `name`,
  `description`, `license`, `compatibility`, `metadata` and `allowed-tools`. That's fine for
  local Claude Code skills. For portable skills, put them under `metadata`.

## C. Writing the body

- **C1. Add only what the agent doesn't already know.** Test each line: "Would the agent get
  this wrong without it?" If not, delete the whole sentence. Don't explain what a PDF is.
- **C2. A Gotchas section is usually the most valuable part.** Concrete facts that go against
  reasonable guesses ("the `users` table soft-deletes; always filter `deleted_at IS NULL`").
  Every time you correct the agent, add a gotcha.
- **C3. Give one default with an escape hatch, not a menu.** "Use pdfplumber. For scanned PDFs,
  use pdf2image + pytesseract."
- **C4. Match strictness to risk.** On a narrow bridge (migrations, official forms), give exact
  commands and say "don't change the flags". In an open field (design, review), give the goal
  and explain *why*.
- **C5. Match the instruction to the failure** (obra's table):

| What the agent does wrong (seen in a no-skill test run) | What to write |
|---|---|
| Knows the rule, skips it under pressure | A prohibition, plus a table of excuses and answers, plus a red-flags list |
| Output has the wrong shape | A positive recipe or template: "the output IS: A, then B, then C" |
| Leaves out a required part | A required slot in the template |
| Should behave differently in some cases | An "if [something visible] then..." rule |

  Avoid "Don't X unless it matters"; that kind of exception clause made results inconsistent in
  obra's tests.
- **C6. Explain the reason** ("Do X because Y causes Z") instead of capital-letter commands. If
  you catch yourself writing ALWAYS or NEVER, treat it as a warning sign.
- **C7. Every step ends with a clear "done" test.** "Every field in `form_fields.json` mapped"
  beats "understand the form". A vague end point invites the agent to stop early.
- **C8. Patterns that work:** a copyable progress checklist; validation loops (do, validate,
  fix, repeat); plan, then validate, then execute for batch or destructive work (write
  `values.json`, check it against the source of truth, then apply); output templates; one
  excellent example rather than many weak ones.
- **C9. Keep terms consistent.** Pick one word per concept and reuse it. mattpocock calls these
  "leading words": short words the model already understands, such as *tight* or *red*.
- **C10. Nothing that goes out of date.** No "if before 2025...". Use a collapsed "Old patterns"
  section instead. Keep each fact in exactly one place, and don't copy what `--help` or a config
  file already says.
- **C11. If a rule must hold every time, use a hook, not prose.** Prose fades over a long
  session; a hook runs on every event.

## D. References vs scripts vs assets

| Use | When |
|---|---|
| **Inline in SKILL.md** | Principles, gotchas, code under ~50 lines, anything every run needs |
| **references/** | Big API docs, schemas, per-variant guides, long templates, loaded only when a pointer fires |
| **scripts/** | Anything deterministic, fragile or repeated. **Signal:** in eval transcripts, every run wrote its own `build_chart.py`, so write it once and ship it |
| **assets/** | Files copied into the output (DOCX templates, fonts, logos, image frames) |

Script rules (agentskills.io and Anthropic):
- No interactive prompts. Take input by flag, env var or stdin.
- `--help` explains usage.
- Errors say what's wrong, what was expected and what to try.
- Data goes to stdout as JSON/CSV; progress and warnings go to stderr.
- Safe to run twice; `--dry-run` for anything destructive; distinct exit codes.
- Keep output small (agent tools cut off at roughly 10-30K characters).
- Pin versions (`npx eslint@9.0.0`) and declare dependencies inline (PEP 723 + `uv run`).
- Handle errors in the script instead of leaving them to Claude.
- Comment every constant ("no magic numbers").
- Forward slashes only.
- Name MCP tools with their server (`Server:tool_name`).

## E. How the best authors test skills

Four layers, from cheapest to most expensive:

1. **Structure (free, every change).** Frontmatter, name rules, length, links resolve. Tools:
   `skills-ref validate`, skill-creator `quick_validate.py`,
   `claude plugin validate ~/.claude/skills`.
2. **Trigger evals: does it fire on the right requests?** (skill-creator `run_loop.py`;
   agentskills "optimizing descriptions")
   - About 20 realistic requests: 8-10 that should fire, 8-10 that shouldn't.
   - The "shouldn't" ones must be **near misses**: same words, different job. "Fix the formulas
     in my Excel budget" for a CSV skill, not "write fibonacci".
   - Make them messy: file paths, back-story, typos, casual language.
   - Run each **3 times** and compute a fire rate; a request passes at >=0.5.
   - **Split 60/40** into tuning and held-out sets, and pick the description that scores best
     on the **held-out** set. Five rounds is usually enough.
   - Note: trivial one-step requests never fire skills, so don't test with them.
3. **Behaviour evals: is it better than having no skill?** (skill-creator)
   - Start with 2-3 realistic prompts in `evals/evals.json`.
   - In the same turn, launch one fresh subagent **with the skill** and one **without it** (or
     with the old version: snapshot it first with `cp -r`).
   - Save the token count and duration of each run straight away; they aren't stored anywhere
     else.
   - Write assertions *after* seeing the first outputs. They must be objectively checkable,
     neither trivial nor brittle.
   - The grader passes something only on concrete evidence and also critiques the assertions
     themselves.
   - Compare with-skill and without-skill on pass rate, time and tokens.
   - Delete assertions that pass in both versions; they don't tell the two apart.
   - **Read the run logs, not just the outputs.**
   - Have a human review the outputs in the viewer and save `feedback.json`. Empty feedback
     means good.
   - Repeat until the feedback is empty or progress stalls.
   - For "is v2 really better?", run a **blind A/B comparison** with `agents/comparator.md`.
4. **Pressure tests, for rule-following skills** (obra `testing-skills-with-subagents`)
   - **RED:** run a scenario *without* the skill and record the agent's excuses word for word.
   - Scenarios combine **3+ pressures** (time, sunk cost, authority, tiredness, looking
     dogmatic), use real paths, and force an A/B/C choice: "You MUST choose and act."
   - **GREEN:** write just enough to counter those exact excuses.
   - **REFACTOR:** each new excuse gets an explicit counter, an entry in the excuse table and a
     red-flag line.
   - **Meta-test:** ask the agent "How could the skill have been written so you'd have chosen
     A?"
   - **Wording micro-tests:** 5+ fresh samples per wording, plus a no-guidance control. If the
     control doesn't show the failure, write nothing. Read every flagged match by hand.

Also: test on every model you'll use, since Haiku needs more detail and Opus less. Pin the
model and the Claude Code version when you report numbers (addyosmani saw fire rates move
between CLI versions). In Claude Code, `claude plugin eval` gives with/without numbers for
skills packaged as a plugin.

## F. Anti-patterns

- A skill written by an LLM from general knowledge with no real task behind it. You get "handle
  errors appropriately". **Extract from a real session instead** (Anthropic's "Claude A writes,
  Claude B tests").
- A description that summarises the steps, says "I can help...", is vague ("helps with
  documents"), or grows into a long list of trigger phrases.
- Heavy capitals (MUST, NEVER, CRITICAL), emphasis with no "because", numeric word caps, "think
  step by step" scaffolds.
- Menus of equal options; examples in five languages; story-style examples ("in session
  2025-10-03 we found...").
- Deeply nested references; `@` force-loads; the same fact in SKILL.md and a reference file;
  time-sensitive text.
- Untested edits, or writing many skills in a batch without testing each one (obra's iron law:
  "no skill without a failing test first").
- Scripts with prompts, unexplained constants, bare `scripts/x.sh` calls (fail when the
  executable bit is lost), Windows paths, assuming packages are installed.
- Orchestration (addyosmani `orchestration-patterns.md`):
  - router agents that only pass messages along;
  - an agent persona that calls another persona;
  - orchestrators that run spec -> plan -> build for you and remove your checkpoints;
  - nesting deeper than one level.
- "Doubt theatre": running reviews where no finding is ever acted on.

## G. Security notes

- **Only install skills from sources you trust, and read every file first** (SKILL.md, scripts,
  images). Look for network calls, file access or tool use that doesn't fit the stated purpose.
  Install counts and stars (Vercel's `find-skills` thresholds: 1K+ installs, 100+ stars) help,
  but aren't proof.
- **Skills that fetch URLs are the riskiest.** Fetched pages can carry injected instructions,
  and dependencies change after you've reviewed them. Pin versions.
- **Treat content as data, not commands** (addyosmani's trust levels):
  - Trusted: your own code.
  - Check before acting on: configs, fixtures, external docs.
  - Untrusted: user uploads, API responses, web pages. Instruction-like text in these is
    something to show the user, not something to obey.
- **Hooks** declared in a skill's `hooks` field register when it fires and **keep running for
  the rest of the session**. Review them like code, and don't install skills with hooks from
  unknown authors.
- **`` !`command` `` lines** run *before* Claude sees the skill. They're checked against
  permission rules, and a deny rule stops the skill. `allowed-tools` pre-approves tools for that
  turn only. Keep both lists narrow.
- **Side-effect skills** (deploy, publish, send) should be `disable-model-invocation: true` so
  Claude can't decide to ship on its own.
- **Cross-model or external-CLI review:** run it read-only, pass the prompt through a file on
  stdin (never inside shell quotes), and get approval every time.
- **Handoff and log files:** redact keys, passwords and personal data. Keep real personal
  identifiers (ID numbers, service numbers) out of evals, fixtures and handoffs; use sample
  data.
- **Principle of no surprise:** a skill's behaviour should match its description. No malware or
  hidden data collection.

## H. Chaining skills into workflows

- **Chain with explicit handoffs at the end of each skill:**
  `REQUIRED SUB-SKILL: use writing-plans`. Name the next skill; don't paste its contents.
- **Pass work through files on disk, not chat memory.** design doc -> spec -> plan -> ledger ->
  review package. After compaction, trust the ledger and `git log` over what you remember.
- **Human checkpoints at judgement points** (approach chosen, spec approved, plan approved,
  ship). **No checkpoints during execution.** Make decisions and log each one as
  `Ruling: what - why - cost if wrong`. Stop only for four things: irreversible actions,
  security, outside side effects (push, publish, merge), or a plan so broken that every path is
  a guess.
- **One fresh subagent per task**, with exactly the context you build for it.
- **Reviewers get the artifact plus the requirements, never your reasoning or your verdict.**
  The prompt says "find what's wrong; don't validate".
- **Cap review loops at about 3 rounds,** then escalate to the user.
- **Close the loop with a retro:** mechanical mistakes become scripts or hooks; judgement
  mistakes become gotchas and new eval cases.

The three reference chains:
- **obra:** brainstorming -> writing-plans -> subagent-driven-development (or executing-plans)
  -> requesting-code-review -> verification-before-completion -> finishing-a-development-branch
- **mattpocock:** grill-with-docs -> (prototype via /handoff) -> to-spec -> to-tickets ->
  implement (tdd + code-review) per ticket, clearing context between tickets -> pr -> retro
- **addyosmani:** SPECIFY -> PLAN -> TASKS -> IMPLEMENT with a human gate at each, plus
  doubt-driven review during the work and code-review at the end

---

# 2. SKILL.md template

```markdown
---
name: doing-the-thing            # = folder name; lowercase-hyphen; <=64
description: >-
  [Domain + concrete outputs, nouns]. Use when [situation 1], [situation 2],
  or [situation 3], even if the user [doesn't name X / pastes it inline / writes in another language].
  Not for [near-miss] (use [sibling-skill]).
# Claude Code only (remove for portable skills, or move under metadata:)
# disable-model-invocation: true   # side effects: publish/send/deploy
# argument-hint: "[file] [format]"
# allowed-tools: Bash(python3 scripts/*) Read
---

# Doing The Thing

[1-2 sentences: what good looks like and why it matters. Most important rules go here, near the top.]

## Gotchas
- [Fact that goes against a reasonable guess, and what to do instead]
- [Correction you had to make in a real run]

## Workflow
Copy this checklist and tick it off:
- [ ] 1. [Action] -> done when [checkable condition]
- [ ] 2. Run `python3 scripts/validate.py out/` -> done when exit 0
- [ ] 3. If validation fails: read the error, fix, re-run step 2
- [ ] 4. [Deliver] -> done when [evidence shown to user: file path / screenshot]

## Output format
[Short template here, or: "Use `assets/template.docx`"]

## Example
Input: [realistic]
Output: [realistic, labeled illustrative]

## When to read more
- Read `references/[topic].md` when [specific observable condition].
- Run `python3 scripts/[tool].py --help` for options.

## Next step
When done, [use `reviewing-the-thing` / hand back to the user for approval].
```
Use this template only for rule-following skills (from obra and addyosmani). Add both sections
when a no-skill test run showed the agent skipping the rule:
```markdown
## Common rationalizations
| Excuse | Reality |
## Red flags (stop and restart)
- ...
```

---

# 3. Checklist for reviewing an existing skill

**Triggering**
- [ ] Description names the domain and outputs, has "Use when..." with distinct situations, a
  "Not for..." when siblings overlap, and no step summary.
- [ ] Third person or instruction form; no "I can"; no capital-letter boosters; under 500
  characters, with the key use first.
- [ ] Ran >=10 should-fire and >=10 near-miss requests, 3 runs each; fire rate >=0.5 on
  positives and below that on negatives (held-out set).
- [ ] Invocation is right: side effects -> user-only; background knowledge ->
  `user-invocable: false`.
- [ ] Name is valid, matches the folder and says what it does; not `helper`.

**Structure and size**
- [ ] Body under 500 lines (often-used skills under ~500 words); top-priority rules in the first
  screen.
- [ ] References one level deep; each pointer says *when* to read; files over 300 lines have a
  table of contents; no `@` force-loads.
- [ ] Every fact lives in one place; nothing time-sensitive; no copies of `--help` or config.
- [ ] Spec validator passes, or Claude Code-only fields are a deliberate choice.

**Content quality**
- [ ] Each paragraph passes "would the agent get this wrong without it?"
- [ ] Gotchas section exists and is concrete.
- [ ] One default per choice; strictness matches risk; reasons given ("because...").
- [ ] Instruction form matches the failure type (recipe for shape, prohibition plus excuse
  table for discipline, slot for omissions).
- [ ] Every step has a checkable "done" condition; there's a final verification step with
  evidence.
- [ ] One realistic example; consistent terms.

**Scripts and assets**
- [ ] Repeated work is a script; scripts are non-interactive, have `--help`, clear errors, JSON
  on stdout and diagnostics on stderr, are safe to re-run, and use `--dry-run` where
  destructive.
- [ ] Dependencies declared or pinned; called through the interpreter; forward slashes;
  constants explained.

**Testing**
- [ ] `evals/evals.json` has 2-3+ realistic prompts with assertions that tell versions apart.
- [ ] Compared with-skill vs no-skill (or old version) on pass rate, tokens and time; logs read.
- [ ] Rule-following skills pressure-tested (3+ pressures); excuses recorded and countered.
- [ ] Tested on the models you actually use.

**Security**
- [ ] No unexpected network calls or file access; fetched content treated as data; versions
  pinned.
- [ ] Hooks, `!` commands and `allowed-tools` reviewed and kept narrow.
- [ ] No secrets or personal data in the skill, evals, fixtures or handoffs.

**Chaining**
- [ ] Names its next skill explicitly; work is passed through files; human checkpoint at
  judgement points only.

---

# 4. Proposed workflow chain for a one-person "software company"

The human stays the orchestrator at four checkpoints (✋); everything between them runs without
stopping.

```
/company (router, user-invoked: maps every skill -> which one when)
   |
1. intake        (grill-style, model-invoked)  -> brief.md
   one question at a time, plain language, recommended answer per question;
   agent looks up facts itself, asks only decisions                 ✋ "yes, that's what I want"
2. spec          -> SPEC-<id>.md : objective, users, acceptance criteria,
   commands, boundaries (Always / Ask first / Never)                ✋ approve spec
3. plan          -> plans/<date>-<id>.md : tasks w/ exact files, test names,
   verify commands, "Review focus" (5 likely failure inputs)        ✋ approve plan + pick mode
4. build         fresh subagent per task, TDD red->green, ledger.md with Rulings;
   stops only for: irreversible / security / publish / broken plan
5. verify        run every command, screenshots (Playwright), evidence or no claim
6. review        fresh-context reviewers given artifact + spec only:
                 - code (spec + quality)  - design review  - domain checker
                 (language / official format / asset spec); <=3 rounds
7. ship          /ship, /publish, /send - disable-model-invocation   ✋ human runs it
8. retro         same session: new gotchas -> the skill; new eval case -> evals.json;
                 mechanical misses -> script/hook
```

How common skill families fit this chain:
- **Web apps:** the full chain. A design-review skill sits at step 6.
- **Official paperwork / forms:** a strict-steps skill. Official templates go in `assets/`, the
  field rules go in `references/`, and a `validate_fields.py` checks plan -> validate -> fill.
  Use sample data only in evals.
- **Tutoring or explainer videos:** intake -> spec (learning goal, length, audience) -> script ->
  storyboard -> render. The checklist gate checks that the script matches the syllabus.
- **Sticker or image packs for a platform:** spec -> generate -> a script that checks every
  image against the platform's official size and format rules (kept in `references/`) ->
  user-only publish.
- **Avatar or visual styling:** an open-field skill (lower strictness). Keep a few varied,
  illustrative examples, and use human-review evals instead of assertions.

**Upgrade order for an existing skill library:**
1. List every skill and mark each one model-invoked or user-only, then build `/company`.
2. Rewrite the descriptions (biggest payoff, cheapest change) and run trigger evals on the 10
   most-used skills.
3. For each skill: run a no-skill test, rewrite with the template, compare with-skill vs
   no-skill, then add gotchas from real use.
4. Turn any work you keep repeating into scripts.

---

# 5. Sources read and failed URLs

**Read in full or in part:**
- **anthropics/skills:** skill-creator (SKILL.md, grader agent, `quick_validate`, `run_eval`,
  `improve_description`), mcp-builder (+ `evaluation.md`), claude-api
  (+ `shared/prompt-audit.md`)
- **obra/superpowers:** writing-skills (+ `testing-skills-with-subagents`, `discovery`,
  `bulletproofing`), brainstorming, writing-plans, executing-plans,
  subagent-driven-development (+ task-reviewer prompt), verification-before-completion,
  using-superpowers, hooks
- **mattpocock/skills:** writing-for-agents (+ `SKILL-MECHANICS`), grill-me / grilling, handoff,
  to-spec (the old to-prd), ask-matt, software-factory, CLAUDE.md
- **addyosmani/agent-skills:** context-engineering, spec-driven-development,
  doubt-driven-development, `evals/README`, `docs/skill-anatomy`,
  `references/orchestration-patterns`
- **vercel-labs/skills:** find-skills, `docs/creating-skills.md`, README
- **agentskills/agentskills repo:** `specification.mdx`, best-practices, evaluating-skills,
  optimizing-descriptions, using-scripts
- **Live pages:** platform.claude.com Agent Skills best-practices and overview (security
  section); code.claude.com skills docs (frontmatter fields, limits, troubleshooting)

**Failed URLs:**
- `https://agentskills.io/specification` was blocked by the network proxy (403). The same spec
  was read from its source in the agentskills/agentskills GitHub repo instead.

**Not used:** obra has no separate `testing-skills-with-subagents` skill; it now lives inside
writing-skills as a reference file, and that's the file read. mattpocock renamed `to-prd` to
`to-spec`.
