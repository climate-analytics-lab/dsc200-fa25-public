# FA26 implementation plan (DRAFT)

Per-module plan for building the course: what carries over from FA25, what is new, and the decisions still open. Companion to [`SYLLABUS.md`](SYLLABUS.md).

## Guiding principles

1. **Teach the judgment, automate the syntax.** Every topic is framed as "what do you need to know to *steer and verify*," not "what do you need to memorize."
2. **Agents in the room from day 1.** Students use a real harness throughout; the course models good practice rather than describing it.
3. **Assessment must survive the tools it teaches.** If an assignment can be completed by pasting it into an agent with no judgment applied, it is a bad assignment. Grade specs, tests, validation reports, and defenses.
4. **Reuse FA25 where reading fluency is the goal**; build new where agent workflow is the goal.

## Module A — Foundations (Weeks 1–3)

**Carries over (condensed):** Lectures 2–4 (Python), 6–8 (NumPy — merge three lectures into one), 9–12 (Pandas + visualization — merge four into two), 17–18 (xarray — merge into the stack overview). Lecture 5 (regex) becomes a half-lecture or reading; agents write regexes, students verify them.

**New to build:**
- Day-1 live demo + lab: build a small analysis with an agent, then a guided dissection of the transcript (what context did it have, what did it assume, where could it be wrong).
- Setup guide: uv/conda, Git/GitHub (+ GitHub Education), Claude Code install and login, permissions defaults for coursework.
- "Bug hunt" notebook per library: agent-generated Pandas/NumPy/xarray code containing realistic silent errors (broadcasting, misalignment, NaN, dtype/timezone); students find and explain them. These become the in-class verification exercise bank.

**Datasets:** reuse `data/` from FA25 (taxi, meteorites, TSA travel, CO2, global temperature NetCDFs) — already sized and licensed for teaching.

**Assignment 1 (Weeks 2–3):** small data-wrangling task delivered twice: once by hand on a subset (reading fluency), once agent-built on the full data with a one-page validation report reconciling the two.

## Module B — Using coding agents (Weeks 4–6)

**All new.** Anchor texts: Ng's "Using coding agents" letter; Anthropic docs on Claude Code and agent security.

**To build:**
- **Week 4 lecture pair:** (a) LLM foundations for users — tokenization, context windows, sampling, tool calling, cutoffs; (b) anatomy of a harness — system prompt, tool loop, permissions, context management; trace a real Claude Code session step by step. Note: keep ML internals out (covered by other DSC courses); focus on behavioral consequences (why it hallucinates APIs, why context placement matters, why caching changes cost).
- **Week 5 workshop:** the spec → plan → implement → verify loop on a shared task. Deliberate contrasts: same task with a vague vs. precise spec; with and without a test suite the agent can run. Introduces evaluation-driven development.
- **Week 6 lecture + lab on security/cost/data:** live prompt-injection demo (malicious README/data file steering an agent); sandboxing and permission modes; secrets hygiene (.env never in context); API cost accounting exercise (estimate then measure token spend for a task); when data cannot leave your machine.
- A course `CLAUDE.md` / agent-config template students adopt in their own repos (test commands, style, guardrails) — makes "harness configuration" a graded, concrete artifact.

**Assignment 2 (Weeks 4–5):** spec-writing. Given a stakeholder email (deliberately loose, e.g. "the dean wants a dashboard of enrollment trends"), produce a spec + acceptance criteria + eval plan; then implement it with an agent. Grade the spec and validation, not the polish.

**Assignment 3 (Week 6):** red-team lab. Each team gets a working agent setup and must (a) demonstrate one injection/exfiltration risk in a sandboxed environment we provide, and (b) harden the config against it. (Scoped, sandboxed, defensive-security framing.)

**Infrastructure decisions needed:** see Open Questions 2–3.

## Module C — SE fundamentals (Weeks 7–9)

**Carries over (refocused):** Lecture 19 (scripting/scikit-learn → scripting/packaging only), Lecture 20 (OOP — reframed as "when structure earns its keep"), Lecture 24 (time complexity — kept as the one algorithmic lecture). Lectures 21–23, 25–26 (stacks, BST, heaps, graphs, sorting PDFs) are **dropped as implementation topics** and compressed into a single "data structures as vocabulary" segment in Week 8. *(Flagged as Open Question 1.)*

**To build:**
- Architecture lecture with 2–3 worked case studies (e.g., one-off analysis vs. nightly pipeline vs. shared package of the same climate calculation) making cost/scalability/reliability/speed trade-offs concrete.
- Flexibility-vs-structure workshop: give teams the same working prototype and diverging change requests; those who over- or under-structured feel it. (This is the BA experience distilled into a lab.)
- Testing lecture pair: pytest, property-based testing (hypothesis), regression/golden tests, data validation (pandera or similar), GitHub Actions CI. Lab: write a test suite that *catches* a planted bug in agent-generated code, then hand the failing suite to the agent to fix — closing the verifier loop from Week 5.
- PR-review exercise: students review an agent-authored pull request on the course repo using a provided rubric.

**Assignment 4 (Weeks 8–9):** refactor + test. Take a messy but working notebook (supplied), turn it into a structured, tested, CI-passing package using an agent; submit the architecture rationale (one page: trade-offs chosen and rejected).

## Week 10 — Shaping the build + project

- Lecture: deciding what to build — synthesizing user signals, iterating when prototypes take a day, speed/cost/risk/human-effort trade-offs, definition of done. Guest speaker candidate: a practicing PM/BA or AI-engineering lead.
- Remaining sessions: project demos + oral defenses.

**Project timeline (runs Weeks 4–10):** W4 teams + brief chosen · W5 spec & eval plan due (graded gate) · W7 architecture + test plan due · W9 code freeze, peer review exchange · W10 demo + defense. Defense format: 10 min demo, then questions targeting whether *they* understand and can justify what their agent built.

## Grading infrastructure

- Rubrics for specs, validation reports, and defenses (new — these carry most of the weight).
- Agent-transcript submission mechanism (session links or exported logs attached to Gradescope/Canvas submissions).
- Autograded components should themselves be eval suites students can run — dogfooding evaluation-driven development.

## Open questions for iteration

1. **DS&A depth:** draft compresses stacks/BST/heaps/graphs/sorting (6 FA25 lectures) into ~1. Is any of it load-bearing for downstream DSC courses that expect DSC 200 to cover it?
2. **Harness standardization & funding:** standardize on Claude Code (consistent teaching, needs API/subscription budget or edu program) vs. tool-agnostic (equitable but fragments instruction)? What per-student token budget is realistic for assignments + project?
3. **Compute/sandbox environment:** UCSD DataHub vs. GitHub Codespaces vs. student laptops for agent labs — the injection/red-team lab in particular needs isolation.
4. **Closed-AI assessment share:** are 2–3 short in-class verification exercises enough to certify reading fluency, or is a sit-down final needed?
5. **Pace risk:** Module A in 3 weeks assumes students accept "read fluently, don't memorize." Fallback: steal a Week 4 session if the Week 3 bug-hunt scores are weak.
6. **Lecture count/cadence:** schedule above assumes ~26 sessions as in FA25 — confirm FA26 meeting pattern before slotting lectures to dates.
