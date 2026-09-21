# DSC 200: Data Science Programming — Fall 2026 (DRAFT syllabus)

**Instructor:** Duncan Watson-Parris
**Format:** ~26 lecture sessions over 10 weeks (schedule TBD), hands-on, bring a laptop
**Prerequisites:** none assumed; graduate standing

## Course description

Programming for data science in the age of coding agents. Most working code is now produced by steering AI agents from loosely defined requirements — business, research, or product — rather than by hand-writing library calls. What remains scarce is the judgment around the code: turning ambiguous requirements into precise specifications, choosing structures and architectures with the right trade-offs, validating that generated code and its outputs are actually correct, and knowing when a project is *done*. This course teaches Python and the PyData ecosystem at the fluency level needed to **read, verify, and steer**, then focuses on the durable engineering skills identified in Andrew Ng's AI Engineering Skills Map: using coding agents, software engineering fundamentals, and shaping the build.

## Learning outcomes

By the end of the course, students can:

1. Read and critically review Python data science code (NumPy/Pandas/xarray/matplotlib) well enough to spot incorrect logic, silent data errors, and misuse of the libraries — whether written by a human or an agent.
2. Operate a coding agent effectively: configure a harness, manage context, scope tasks, trade off planning vs. execution, and close the loop with verifiers.
3. Translate vague stakeholder requirements into specs, acceptance criteria, and evaluation plans; decide what to build next from feedback; recognize "done."
4. Make and defend software design decisions: flexibility vs. structure, architecture patterns, data storage, and cost/scalability/reliability/speed trade-offs.
5. Design testing and validation strategies appropriate to AI-generated code: unit/property/regression tests, data validation, statistical sanity checks, CI.
6. Use agents responsibly: sandboxing and permissions, secrets hygiene, prompt injection awareness, data governance, and cost/latency budgeting.
7. Explain, at a working level, how an LLM-based coding agent functions (tokens, context windows, tool calling, the agentic loop) and why the harness matters as much as the model.

## Course structure (10 weeks)

### Module A — Foundations for reading and verifying code (Weeks 1–3)

*Compressed from ~12 FA25 lectures to ~7. The goal is fluency in reading and mental models, not API recall.*

- **Week 1 — Orientation & tooling.** Why this course changed; the AI Engineering Skills Map; what "programming" means in 2026. Setup: Python environments, Git/GitHub, notebooks, and a coding-agent harness (Claude Code). First contact: build something small with an agent on day one, then dissect what it did.
- **Week 2 — Python essentials.** Syntax, data types, control flow, functions, comprehensions, errors/exceptions — taught through *reading and debugging* code (including agent-generated code) as much as writing it. Scripts vs. notebooks; modules and imports.
- **Week 3 — The PyData stack as mental models.** NumPy (arrays, vectorization, broadcasting), Pandas (indexes, alignment, group-by, tidy data), xarray (labeled multi-dimensional data), matplotlib (figure anatomy). Emphasis on the failure modes agents commonly introduce: silent broadcasting bugs, index misalignment, NaN propagation, dtype/timezone traps, chained-assignment surprises.

### Module B — Using coding agents (Weeks 4–6)

*New for FA26. Based on the "Using coding agents" and parts of "Building and deploying AI applications" skill areas.*

- **Week 4 — How the machine works (just enough).** LLM foundations for users: tokenization, context windows, sampling, knowledge cutoffs, tool/function calling. The agentic loop: model + harness (system prompts, tools, permissions, memory/context management). Why the harness is as much of the product as the model. Case study: what Claude Code actually does between your prompt and the diff.
- **Week 5 — The agentic workflow.** Requirements → spec → plan → implement → verify. Scoping tasks; when to plan vs. when to let the agent run; reviewing diffs; giving the agent verifiers (tests, evals, type checks) so it can close loops autonomously. Evaluation-driven development. Managing context deliberately: what to put in, what to keep out, when to start fresh.
- **Week 6 — Security, cost, and data constraints.** Sandboxing and permission models; keeping secrets and credentials out of agent context; prompt injection and untrusted data; working with sensitive or licensed data; cost and latency budgets; reproducibility of agent-assisted work; logging and audit trails.

### Module C — Software engineering fundamentals for data science (Weeks 7–9)

*Refocuses FA25's OOP + data-structures block toward design judgment. Based on the "Software engineering fundamentals" skill area.*

- **Week 7 — Structuring code.** From notebook to script to module to package. Interfaces and contracts; functions vs. classes; OOP where it earns its keep. The central trade-off: flexibility vs. structure — when to generalize, when to hard-code, and how much structure to impose on agent-written code.
- **Week 8 — Architecture and trade-offs.** Data pipelines and DAGs; layered designs; choosing data stores and file formats (CSV/Parquet/NetCDF/Zarr/databases); cost–scalability–reliability–speed trade-offs. Complexity and data structures as *vocabulary for reasoning* (Big-O, arrays vs. hash maps vs. trees) rather than implementation exercises.
- **Week 9 — Testing and validation.** What to test when you didn't write the code: unit, property-based, and regression tests; golden datasets; schema and statistical validation of data outputs; CI on GitHub; code review as the primary human act. Reviewing an agent's PR.

### Week 10 — Shaping the build

*Capstone week. Based on the "Shaping the build" skill area.*

- Turning stakeholder language into buildable scope (the business-analyst skill); synthesizing user signals into fast product decisions; iterating when prototypes take a day, not a month; speed–cost–risk–human-effort trade-offs; definition of done.
- Final project demos and design defenses.

## Assessment (draft — percentages TBD)

| Component | Weight | Notes |
|---|---|---|
| Participation (in-class polls/activities) | ~10% | as in FA25 |
| Assignments (×4) | ~40% | spec + agent-built implementation + **validation report** + agent transcript |
| In-class verification exercises (×2–3) | ~15% | short, closed-AI: read/debug/review code by hand — keeps outcome 1 honest |
| Quarter-long project | ~35% | staged: proposal/spec → architecture & test plan → build → demo + oral defense |

**AI policy (inverted from FA25):** Use of coding agents is *expected and taught*. All agent use must be disclosed and logged (transcripts/session links submitted with work). You are accountable for everything you submit: "the agent wrote it" is not a defense — validating it was the assignment. Closed-AI exercises are explicitly marked.

**Project:** teams of 2–3 take a loosely specified, realistic brief (real datasets — e.g., climate and transportation data from the course repo — or a stakeholder brief of their own) from requirements to a validated, tested, documented data product built primarily with coding agents. Graded artifacts are the spec, the test/eval suite, the review history, and the defense — not lines of code written.

## Logistics (placeholders)

- Websites: Canvas (syllabus of record), GitHub (materials), ClassBuzz (participation)
- Office hours, TA list, schedule of record: TBD
- Academic integrity: UCSD policy applies; undisclosed AI use is an integrity violation under the disclosure policy above.

## Key references

- A. Ng, *The AI Engineering Skills Map* and the four "in detail" letters (The Batch, DeepLearning.AI, Aug–Sep 2026): overview; using coding agents; software engineering fundamentals; building and deploying AI applications; shaping the build.
- Anthropic, Claude Code documentation (harness, permissions, hooks) — https://code.claude.com/docs
- Course texts from FA25 remain optional references for the PyData stack.
