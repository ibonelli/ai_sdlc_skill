# AI Workflow for SDLC

Assuming the Software Development Life Cycle (SDLC) will change with AI, we started working on getting this going for 

**Triger**: How to use Copilot (or other AI helpers) for development engenieering: Scouting, reading rules for the project, writing a plan, etc... Also working on distilling the context for the task and rules when working on changes.

There **is solid, experience‑based guidance online**, and more importantly there is a **clear convergence of practices** across teams that are using Copilot / LLMs *seriously* for software engineering (not just code completion). Below is a **critical, practitioner‑oriented map** of what works, what doesn’t, and where to learn from teams that have already fallen into the holes.

I’ll structure this into:

1.  **What mature teams actually use AI for (beyond coding)**
2.  **Repeatable working patterns (scouting → rules → plan → change)**
3.  **How teams “distill context” without losing discipline**
4.  **Online sources worth reading (case studies & doctrine)**

## Table of contents

- [AI Workflow for SDLC](#ai-workflow-for-sdlc)
  - [Table of contents](#table-of-contents)
  - [AI Design](#ai-design)
    - [1. What teams *actually* use AI for (beyond writing code)](#1-what-teams-actually-use-ai-for-beyond-writing-code)
    - [2. A practical workflow that actually works](#2-a-practical-workflow-that-actually-works)
      - [Phase 1 – Scouting / orientation](#phase-1--scouting--orientation)
      - [Phase 2 – Reading rules \& constraints](#phase-2--reading-rules--constraints)
      - [Phase 3 – Writing the plan (this is the big win)](#phase-3--writing-the-plan-this-is-the-big-win)
      - [Phase 4 – Executing changes safely](#phase-4--executing-changes-safely)
    - [3. Context distillation: where most teams fail](#3-context-distillation-where-most-teams-fail)
      - [Common failure mode](#common-failure-mode)
      - [What actually works (context engineering)](#what-actually-works-context-engineering)
    - [4. Online sources that are actually worth your time](#4-online-sources-that-are-actually-worth-your-time)
    - [Important things to keep in mind](#important-things-to-keep-in-mind)
  - [AI Planning \& Artifacts](#ai-planning--artifacts)
    - [1. Proposed phase model (slightly refined)](#1-proposed-phase-model-slightly-refined)
    - [2. Phase-by-phase artifacts (inputs \& outputs)](#2-phase-by-phase-artifacts-inputs--outputs)
      - [Phase 1 — Scoping](#phase-1--scoping)
      - [Phase 2 — Requirements \& Constraints](#phase-2--requirements--constraints)
      - [Phase 3 — Planning \& Design](#phase-3--planning--design)
      - [Phase 4 — Data \& Architecture](#phase-4--data--architecture)
      - [Phase 5 — Execution](#phase-5--execution)
      - [Phase 6 — Testing \& Validation](#phase-6--testing--validation)
      - [Phase 7 — Documentation \& Knowledge Capture](#phase-7--documentation--knowledge-capture)
    - [3. Visual summary (artifact flow)](#3-visual-summary-artifact-flow)
    - [4. Where this aligns with documented industry practice](#4-where-this-aligns-with-documented-industry-practice)
    - [Summary](#summary)
  - [Articles (post investigation research)](#articles-post-investigation-research)

## AI Design

### 1. What teams *actually* use AI for (beyond writing code)

High‑performing teams do **not** treat Copilot as a code writer; they treat it as a **thinking accelerator** across the SDLC:

| Phase              | Real AI usage patterns                                                       |
| ------------------ | ---------------------------------------------------------------------------- |
| Scoping & scouting | Exploring architectures, identifying hidden constraints, alternative designs |
| Reading rules      | Digesting specs, RFCs, ADRs, regulatory text, legacy docs                    |
| Planning           | Turning messy notes into staged execution plans                              |
| Change execution   | Localized code changes with strict constraints                               |
| Review             | Explaining, refactoring, testing, and consistency checks                     |

This is consistent across:

*   GitHub Copilot team documentation and case studies [\[docs.github.com\]](https://docs.github.com/en/copilot/get-started/best-practices), [\[medium.com\]](https://medium.com/@birlla/our-experiment-with-github-copilot-a-practical-guide-for-development-teams-0c1d5ce3d5a4)
*   Thoughtworks’ field experience with AI‑assisted delivery [\[thoughtworks.com\]](https://www.thoughtworks.com/radar), [\[prnewswire.com\]](https://www.prnewswire.com/news-releases/as-ai-accelerates-software-complexity-thoughtworks-technology-radar-urges-a-return-to-engineering-fundamentals-to-combat-cognitive-debt-302737210.html)

**Key insight:**  
Teams get value when AI is used to **reduce cognitive load**, *not* to replace engineering judgement.

### 2. A practical workflow that actually works

This pattern shows up again and again in successful teams.

#### Phase 1 – Scouting / orientation

Use AI to **map the problem space**, not to decide.

Typical prompt shape:

*   “Here is what I understand so far…”
*   “What assumptions am I making?”
*   “What would break at scale / in prod / legally?”

This improves early risk detection, which multiple teams report as one of the highest ROI uses of AI. [\[jellyfish.co\]](https://jellyfish.co/library/ai-in-software-development/use-cases-and-best-practices/), [\[guageai.com\]](https://guageai.com/blog/github-copilot-impact-engineering-teams)

👉 Treat AI as a *hostile reviewer*, not a helper.

#### Phase 2 – Reading rules & constraints

Teams upload:

*   ADRs (Architecture Decision Record)
    - Why did we pick this architecture?
    - Is this constraint intentional or accidental?
    - Can we change this, or will something explode?
*   Coding standards
*   Security policies
*   API contracts
*   Regulatory documents

And ask AI to:

*   Summarize **constraints only**
*   Extract **MUST / MUST NOT**
*   Flag ambiguity or contradictions

This aligns with **spec‑driven prompt engineering** and “rules first” approaches seen in enterprise teams. [\[linkedin.com\]](https://www.linkedin.com/pulse/spec-driven-prompt-engineering-five-part-playbook-reliable-arvind-t-n-21ayc), [\[tobiasduer....github.io\]](https://tobiasduerschmid.github.io/SEBook/development_practices/promptengineering.html)

> If constraints are not explicit in the prompt, they **will be violated**.

#### Phase 3 – Writing the plan (this is the big win)

AI excels at turning:

*   messy notes
*   partial requirements
*   meeting transcripts

into:

*   staged plans
*   checklists
*   validation steps

Teams use AI here *before* writing code, because changing plans is cheaper than changing code. [\[jellyfish.co\]](https://jellyfish.co/library/ai-in-software-development/use-cases-and-best-practices/), [\[metacto.com\]](https://www.metacto.com/blogs/github-copilot-best-practices-from-high-performing-teams)

But:

*   Humans approve the plan
*   Humans own sequencing and trade‑offs

#### Phase 4 – Executing changes safely

Productive teams **narrow context aggressively**:

Instead of:

> “Modify the system to support X”

They use:

*   Limited file scopes
*   Explicit non‑goals
*   Required invariants

GitHub itself advises breaking tasks down and scoping prompts carefully to avoid hallucinated changes. [\[docs.github.com\]](https://docs.github.com/en/copilot/get-started/best-practices)

Some teams go further and:

*   Encode constraints in Copilot instruction files
*   Keep architectural rules next to the codebase [\[dev.to\]](https://dev.to/dimeloper/mastering-ai-assisted-software-development-from-prompts-to-production-ready-code-54n8)

### 3. Context distillation: where most teams fail

This is the hardest part — and where experienced teams diverge from casual users.

#### Common failure mode

Dump *everything*:

*   Entire repo
*   All history
*   Every rule

Result: vague, generic output.

#### What actually works (context engineering)

Modern teams separate context into **layers**:

1.  **Stable context**
    *   Architecture
    *   Design principles
    *   Regulatory rules
2.  **Task context**
    *   What is changing
    *   Why
    *   Acceptance criteria
3.  **Local working set**
    *   Files
    *   APIs
    *   Boundaries

This evolution from “prompt engineering” → **context engineering** is well‑documented and increasingly explicit in modern guidance. [\[magnus919.com\]](https://magnus919.com/2025/07/the-complete-2025-prompt-engineering-guide-from-prompts-to-context/), [\[featherless.ai\]](https://featherless.ai/blog/prompt-engineering-and-context-engineering-the-complete-developers-guide-to-modern-ai-system-design)

Thoughtworks explicitly calls this out as necessary to avoid *cognitive debt*. [\[prnewswire.com\]](https://www.prnewswire.com/news-releases/as-ai-accelerates-software-complexity-thoughtworks-technology-radar-urges-a-return-to-engineering-fundamentals-to-combat-cognitive-debt-302737210.html)

### 4. Online sources that are actually worth your time

Below are **credible, experience‑based references** (not hype).

* **Spec‑Driven Prompt Engineering**  
    LinkedIn deep dive (reliability & governance) [\[linkedin.com\]](https://www.linkedin.com/pulse/spec-driven-prompt-engineering-five-part-playbook-reliable-arvind-t-n-21ayc)
* [OpenAI Model Spec](https://model-spec.openai.com/2025-04-11.html)
* [SE Book](https://tobiasduerschmid.github.io/SEBook/): Collection of Software Engineering concepts by [Tobias Dürschmid](https://tobiasduerschmid.github.io/). Downloadable @ [GitHub](https://github.com/tobiasduerschmid/tobiasduerschmid.github.io/tree/master/SEBook).
* [The SDLC By Claude Code Sonnet 4.5](https://github.com/cloudstreet-dev/The-Software-Development-Life-Cycle): Good destillation of the steps.

### Important things to keep in mind

*   If rules are not explicit, AI **will violate them**
*   If plans are not written before coding, AI **accelerates mistakes**
*   If context is not structured, AI **adds noise not insight**
*   Teams that scale AI usage re‑introduce **engineering discipline**, not less of it

The winning mindset is:

> *AI is a junior engineer with perfect recall and poor judgment.*

## AI Planning & Artifacts

**Triger**: We need create a process and the documentation that we would have as ouput of one phase and input of the next phase. So given for example these development phases/steps: Scoping, Planning, Data Architecture, Execution, Testing, Documenting; what document and the titles of these documents we want to have as input and output.

A **disciplined, artifact‑driven SDLC**, but with two important twists that many teams miss:

1.  Each phase must **produce a concrete document/artifact**
2.  That artifact becomes the **explicit input and constraint** for the next phase (and for AI tools)

Below is a **clean, critical process model** that aligns with:

*   Classical Software Development Life Cycle (SDLC)
*   Thoughtworks / enterprise delivery practices
*   Modern AI‑assisted development
*   What’s realistically maintainable (no ivory‑tower docs)

All document types and transitions are backed by **documented industry practice** (citations included).

### 1. Proposed phase model (slightly refined)

I’ll start from your list and add only what is **strictly necessary** to make it work in real teams.

    Scoping
    → Requirements & Constraints
    → Planning & Design
    → Data & Architecture
    → Execution
    → Testing & Validation
    → Documentation & Knowledge Capture

This is consistent with standard SDLC definitions and enterprise variants. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/), [\[atlassian.com\]](https://www.atlassian.com/agile/software-development/sdlc)

### 2. Phase-by-phase artifacts (inputs & outputs)

#### Phase 1 — Scoping

**Goal:** Decide *whether* and *why* we should do this.

**Key Output Documents:**

*   **Problem Statement / Opportunity Brief**
*   **High‑level Scope Definition**

**Typical contents:**

*   Business problem
*   In‑scope / out‑of‑scope
*   Success criteria
*   Constraints known *at this point*

**Why industry uses this:**  
Feasibility and scope clarification is universally recommended as the first SDLC step. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/)

**AI usage:**  
Scouting, alternative approaches, risk identification.

➡️ **Input to next phase:** *Approved scope & problem framing*

#### Phase 2 — Requirements & Constraints

(This is implicit in your list but must be explicit to avoid chaos.)

**Goal:** Define *what must be true* — not how yet.

**Key Output Documents:**

*   **Requirements Specification (SRS or lightweight equivalent)**
*   **Constraints Register**
*   **Non‑Functional Requirements (NFRs)**

Widely adopted across SDLC frameworks. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/), [\[paceai.co\]](https://paceai.co/software-development-life-cycle-documentation/)

**Critical distinction:**

*   Requirements = what the system must do
*   Constraints = what it must *not violate*

**AI usage:**  
Summarization of policies, extraction of MUST/MUST NOT, gap detection.

➡️ **Input to next phase:** *Approved requirements + constraints*

#### Phase 3 — Planning & Design

**Goal:** Decide *how we intend to deliver*.

**Key Output Documents:**

*   **Delivery Plan / Execution Plan**
*   **High‑Level Design (HLD)**
*   **Architecture Decision Records (ADR – Draft status)**

Design documentation as a distinct phase is standard practice. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/), [\[docs.aws.amazon.com\]](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html)

**Why ADRs explicitly belong here:**

*   This is where **irreversible or costly decisions** happen
*   ADRs capture **why**, not just what

AWS, Google, and Thoughtworks all recommend ADRs at this stage. [\[docs.aws.amazon.com\]](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html), [\[docs.cloud...google.com\]](https://docs.cloud.google.com/architecture/architecture-decision-records)

➡️ **Input to next phase:** *Approved plan + accepted ADRs*

#### Phase 4 — Data & Architecture

(You explicitly called this out — correctly.)

**Goal:** Lock structural decisions that code must follow.

**Key Output Documents:**

*   **Architecture Overview**
*   **Data Model / Data Contracts**
*   **Finalized ADRs (Accepted state)**

Enterprise architecture guidance explicitly treats data & architecture as first‑class artifacts. [\[docs.aws.amazon.com\]](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html), [\[docs.cloud...google.com\]](https://docs.cloud.google.com/architecture/architecture-decision-records)

**Why separate from execution:**

*   Data contracts and architectural rules must be stable
*   Execution without this leads to costly rewrites

**AI usage:**  
Architecture consistency checks, alternative pattern analysis.

➡️ **Input to next phase:** *Architecture & data contracts as hard constraints*

#### Phase 5 — Execution

**Goal:** Build only what was agreed — nothing more.

**Key Output Documents/Artifacts:**

*   **Source code**
*   **Change log**
*   **Updated ADRs (if superseded)**

Execution maps to classic “Development” in SDLC. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/)

**Important reality:**  
If execution requires a change in architecture → **new ADR**, not an undocumented deviation.

➡️ **Input to next phase:** *Runnable system + traceable changes*

#### Phase 6 — Testing & Validation

**Goal:** Prove the system meets requirements and constraints.

**Key Output Documents:**

*   **Test Plan**
*   **Test Cases**
*   **Validation Report**
*   **Acceptance Sign‑off**

Testing artifacts are a mandatory SDLC output across all models. [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/), [\[paceai.co\]](https://paceai.co/software-development-life-cycle-documentation/)

**AI usage:**  
Test case generation, edge‑case discovery, traceability checks.

➡️ **Input to next phase:** *Verified system*

#### Phase 7 — Documentation & Knowledge Capture

(This is where most teams fail — and where you’re clearly aiming higher.)

**Goal:** Make the work **transferable and reusable**.

**Key Output Documents:**

*   **System Documentation**
*   **Operational Runbooks**
*   **Architecture Knowledge Base**
*   **ADR Log (Decision History)**

Long‑term SDLC documentation is critical for maintenance and onboarding. [\[paceai.co\]](https://paceai.co/software-development-life-cycle-documentation/), [\[document360.com\]](https://document360.com/blog/agile-documentation/)

**This is also where AI shines**:

*   Summarizing decisions
*   Producing onboarding‑ready docs
*   Translating technical details for non‑technical audiences

### 3. Visual summary (artifact flow)

```text
Scoping
  → Problem Statement

Requirements
  → SRS + Constraints

Planning & Design
  → Delivery Plan + Draft ADRs

Data & Architecture
  → Accepted ADRs + Data Contracts

Execution
  → Code + Change Log

Testing
  → Test Reports + Sign-off

Documentation
  → Knowledge Base + ADR Log
```

### 4. Where this aligns with documented industry practice

This structure aligns closely with:

*   Classical SDLC models [\[geeksforgeeks.org\]](https://www.geeksforgeeks.org/software-engineering/software-development-life-cycle-sdlc/), [\[atlassian.com\]](https://www.atlassian.com/agile/software-development/sdlc)
*   ADR governance recommended by AWS & Google [\[docs.aws.amazon.com\]](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html), [\[docs.cloud...google.com\]](https://docs.cloud.google.com/architecture/architecture-decision-records)
*   Thoughtworks’ recent **Structured Prompt‑Driven Development** approach (treating specs & prompts as first‑class artifacts) [\[martinfowler.com\]](https://martinfowler.com/articles/structured-prompt-driven/)
*   Agile documentation best practices (lightweight but intentional) [\[document360.com\]](https://document360.com/blog/agile-documentation/), [\[mural.co\]](https://www.mural.co/blog/agile-documentation)

### Summary

What you are designing is:

*   **Not waterfall**
*   **Not “just agile”**
*   **An artifact‑driven pipeline**

This is exactly what teams need when:

*   Working cross‑country
*   Reducing key‑person risk
*   Using AI without losing control

## Articles (post investigation research)

I found these after starting building the architecture:

- From [AI driven SDLC](https://blog.devops.dev/ai-driven-sdlc-how-to-build-secure-governed-and-scalable-software-with-ai-3d71f7294bca) -- PaidWall
  - Links
    - https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/
    - https://aws.amazon.com/es/blogs/apn/transforming-the-software-development-lifecycle-sdlc-with-generative-ai/
    - https://circleci.com/blog/ai-sdlc/
    - https://github.com/awslabs/aidlc-workflows
    - https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html
  - Videos
    - https://www.youtube.com/watch?v=4qcWgPb-8Fk
    - https://www.youtube.com/watch?v=1HNUH6j5t4A
  - Tools
    - https://kiro.dev/
    - https://github.com/bmad-code-org/BMAD-METHOD
- [Harness Engineering](https://ai.gopubby.com/harness-engineering-what-every-ai-engineer-needs-to-know-in-2026-0ab649e5686a): Very useful article which points to another good article...
- [Beyond vibe coding](https://www.thoughtworks.com/insights/blog/generative-ai/beyond-vibe-coding-the-five-building-blocks-of-aI-native-engineering): Lots of tools, links and market options.
- [The 4 Lines Every CLAUDE.md Needs](https://levelup.gitconnected.com/the-4-lines-every-claude-md-needs-2717a46866f6):
    1. Don’t assume. Don’t hide confusion. Surface tradeoffs.
    2. Minimum code that solves the problem. Nothing speculative.
    3. Touch only what you must. Clean up only your own mess.
    4. Define success criteria. Loop until verified.

Looking for tools online aligned with "Software Development Life Cycle (SDLC) Claude Code assistance skill":
- [Claude SDLC Plugin Marketplace](https://github.com/danielscholl/claude-sdlc)
- [How to Build Claude Code Skills](https://fp8.co/articles/Claude-Code-Skills-Complete-Developer-Guide)
- [SDLC Studio](https://github.com/DarrenBenson/sdlc-studio/): Claude Code skill for managing the full software development lifecycle.
- [Claude Agents](https://github.com/technioz/claude-agents): An SDLC automation system using 9 specialized AI agents that work together to build, test, secure, ...
- [SDLC plugin](https://github.com/iamladi/cautious-computing-machine--sdlc-plugin): Full development lifecycle plugin for Claude Code — TDD, code review, testing, and PR automation.
- [Claude Skills: Product Development Lifecycle (PDLC) Role Collection](https://github.com/sethdford/claude-skills): 454 standards-grounded Claude Code skills for every PDLC role.
