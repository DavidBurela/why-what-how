# Lifecycle Playbook

When and how to engage with the Why–What–How structure throughout a project's life.

This is a lifecycle guide — it covers the ongoing activities that keep documentation current and useful. For what to create and in what order during initial setup, see `docs.bootstrap.md`. For the model itself, see `docs.why-what-how.md`. For copy-paste-ready agent prompts for each scenario below, see the [prompt catalog](https://github.com/DavidBurela/why-what-how/blob/main/prompt-examples.md) in the Why–What–How core repository.

## Quick reference

| Event | When it happens | Jump to |
|-------|----------------|---------|
| **Starting points** | | |
| Greenfield project | New project, early discussions | [Greenfield project](#greenfield-project) |
| Existing project — refactor | Restructure scattered docs (preferred) | [Existing project — refactor](#existing-project--refactor) |
| Existing project — distil | Non-disruptive tryout | [Existing project — distil](#existing-project--distil-gentle-alternative) |
| **Lifecycle events** | | |
| Post-envisioning / kickoff | After a discovery or kickoff session | [Jump](#post-envisioning--kickoff) |
| Post-architecture session | After an architecture design session | [Jump](#post-architecture-session) |
| Building system context | When external dependencies are identified | [Jump](#building-system-context) |
| Application decomposition | When breaking down into deployable units | [Jump](#application-decomposition) |
| C4 model generation | When structural diagrams are needed | [Jump](#c4-model-generation) |
| C4 model validation | When solution docs may have drifted | [Jump](#c4-model-validation) |
| BDD scaffolding | When scenarios are ready for verification | [Jump](#bdd-scaffolding) |
| Feature planning (SDD/RPI) | When planning a feature or backlog item | [Jump](#feature-planning-sddrpi) |
| Post-implementation reflection | After completing a feature | [Jump](#post-implementation-reflection) |
| New team member onboarding | When someone joins the project | [Jump](#new-team-member-onboarding) |
| Scope change or pivot | When business direction changes | [Jump](#scope-change-or-pivot) |
| Post-design-research synthesis | After completing user research | [Jump](#post-design-research-synthesis) |

## Starting points

### Greenfield project

You have meeting notes, business context, workshop outputs, etc. and need to distil them into the structure for the first time.

- Place all raw inputs (meeting notes, business problem docs, DT outputs, background) into a scratch folder (e.g. `agent-temp/`). These stay outside the canonical `docs/` structure.
- Point the agent at `docs.bootstrap.md` and your raw inputs.
- Follow the bootstrap phases in order: foundation first (Phase 1), then personas and journeys (Phase 2), then solution (Phase 3).
- Don't skip Phase 1 — even if the solution feels more urgent, anchoring the WHY first prevents tech-first drift.
- If using Design Thinking methods, see the DT mapping table in `docs.bootstrap.md` to identify which business files should be updated from your method outputs.

### Existing project — refactor

The repo has scattered markdown (ADRs, design docs, SDDs, research). You want to consolidate into the Why–What–How structure.

- This is the more common and higher-value path. Refactoring means consolidating scattered docs into the canonical structure, removing redundant files, and updating cross-references.
- Expect an asymmetry: most existing content will map to Solution (WHAT) and Decisions. The Business (WHY) layer is often thin or missing — teams typically haven't captured personas, journeys, or scenarios in structured form.
- Start by having the agent audit the existing repo and map content to the four areas. This produces a refactoring plan before any files move.
- Execute the plan incrementally — move documents to their canonical locations, merge duplicates, update links. Commit after each logical group so the history is traceable.
- For the Business layer: capture what you can infer from existing docs (stakeholders from ADRs, scope from design docs, etc.) and flag gaps to fill later. Placeholder files with a "to be enriched" note are better than missing files.
- Some journeys and scenarios can be inferred from existing user stories, acceptance criteria, or test cases — even if they weren't written in that format.

### Existing project — distil (gentle alternative)

Same scattered repo, but you want to try the structure without disrupting what's there.

- Distilling means keeping existing files in place and creating the canonical structure alongside them, pulling high-signal content into the new docs.
- Lower risk, good for evaluation before committing to a full refactoring.
- The downside is that it leaves redundancy in the repo — two sources of truth until you clean up. Plan to migrate fully or accept the duplication.

## Lifecycle events

| Event | When it happens | What's affected | Who typically drives |
|-------|----------------|-----------------|---------------------|
| Post-envisioning / kickoff | After a discovery or kickoff session | Business foundation | TPM / Designer |
| Post-architecture session | After an architecture design session | Solution context, applications, ADRs | SE |
| Building system context | When external dependencies are identified | Solution context | SE |
| Application decomposition | When breaking down into deployable units | Solution applications | SE |
| C4 model generation | When structural diagrams are needed | C4 model, solution exports | SE |
| C4 model validation | When solution docs may have drifted from the model | C4 model vs solution docs | SE |
| BDD scaffolding | When scenarios are ready for executable verification | BDD feature files | SE |
| Feature planning (SDD/RPI) | When planning implementation of a feature or backlog item | Solution applications, standards | SE |
| Post-implementation reflection | After implementing a feature or resolving a significant issue | ADRs, standards | SE |
| New team member onboarding | When someone joins the project | All areas (read-only orientation) | Any role |
| Scope change or pivot | When business direction changes significantly | Business foundation, scope, outcomes | TPM |
| Post-design-research synthesis | After completing user research | Personas, journeys, scenarios | Designer |

### Post-envisioning / kickoff

**When:** After a discovery session, design thinking workshop, stakeholder alignment meeting, or project kickoff.

**What's affected:** `business-context.md`, `vision.md`, `outcomes.md`, `scope.md`, possibly `assumptions-and-risks.md`.

**Guidance:**

- Place meeting notes and session outputs into a scratch folder.
- Have the agent read the existing business docs and the new inputs.
- Ask it to validate current docs against the new information and propose specific updates.
- If using Design Thinking, see the DT mapping table in `docs.bootstrap.md`.
- Review agent proposals — envisioning outputs often contain nuance that requires human judgement.

### Post-architecture session

**When:** After an architecture design session (ADS), system design review, or significant technical decision.

**What's affected:** `solution-context.md`, `applications-context.md`, application `app-context.md` files, ADRs.

**Guidance:**

- Place session notes and any diagrams/sketches into a scratch folder.
- Have the agent read existing solution docs and the session outputs.
- Focus on: system boundary changes, new/removed applications, changed relationships, new external dependencies.
- If a significant choice was made, create an ADR capturing the decision, alternatives considered, and trade-offs.
- If the C4 model exists, have the agent update `workspace.dsl` to reflect structural changes.

### Building system context

**When:** When the team identifies the external systems the solution depends on or interacts with (data warehouses, payment providers, identity systems, etc.).

**What's affected:** `solution-context.md` (external systems table), `applications-context.md` (relationship details).

**Guidance:**

- Tell the agent what the external systems are, what the interaction/dependency is (inbound vs outbound), and what protocol is used.
- The agent populates the external systems table in `solution-context.md` and integration details in `applications-context.md`.
- Define relationships at the lowest correct level — system-level dependencies in `solution-context.md`, application-specific dependencies in the relevant `app-context.md`.

### Application decomposition

**When:** When the team begins breaking the solution into deployable units (applications).

**What's affected:** Application folders and `app-context.md` files, `applications-context.md`, `solution.index.md`.

**Guidance:**

- Share your initial thoughts on the decomposition — the website, API, worker, database, etc.
- The agent creates application folders with `<app>.index.md` and `app-context.md` for each.
- Each application gets: a short code (for naming conventions), technology summary, capabilities, and dependencies.
- Cross-application relationships go in `applications-context.md`.
- Add the scenario→flow traceability table to `solution.index.md` even if flows aren't written yet.

### C4 model generation

**When:** When the solution structure is stable enough that structural diagrams would be valuable.

**What's affected:** `solution/c4-model/workspace.dsl`, `solution/c4-model/export/`.

**Guidance:**

- Have the agent read `docs.why-what-how.c4model.md` for C4 conventions.
- The agent generates `workspace.dsl` from the solution docs (system context, applications, relationships).
- Dynamic views should be added for flows that have been documented.
- Export diagrams after generation and embed in relevant markdown files.

### C4 model validation

**When:** When solution docs may have drifted from the C4 model, or before a milestone/review.

**What's affected:** `workspace.dsl` and/or solution markdown docs.

**Guidance:**

- Have the agent compare the C4 model against the solution folder — are all applications represented? Are relationships consistent? Are dynamic views current?
- Fix discrepancies in whichever direction is appropriate: update the model if docs are more current, or update docs if the model is more current.
- This is a good periodic hygiene check.

### BDD scaffolding

**When:** When scenarios exist and the team wants executable verification, even before implementation is complete.

**What's affected:** BDD feature files (in test folders, not under `docs/`), scenario files (links to feature files).

**Guidance:**

- Have the agent read `docs.why-what-how.bdd.md` for BDD conventions.
- The agent creates feature file stubs from the documented scenarios — each scenario becomes a feature file with Given/When/Then skeleton.
- Feature files use business language only — no HTTP verbs, no JSON, no API paths.
- These start red (failing). The team turns them green as implementation progresses. This gives a visual progress indicator of business requirements being met.
- Update scenario files with links to the new feature files.

### Feature planning (SDD/RPI)

**When:** A developer is creating an SDD spec, research plan, or planning to implement a feature or backlog item.

**What's affected:** Solution application docs, standards, potentially new flows.

**Guidance:**

- Point the agent at the relevant application definitions and the standards docs.
- Ask it to consider the backlog item or feature being implemented against the existing architecture and conventions.
- The agent can help draft a plan that's consistent with established patterns, identify standards that apply, and flag where new flows or ADRs may be needed.
- This is preventative — catching misalignment before coding starts is cheaper than refactoring after.

### Post-implementation reflection

**When:** After completing a feature, resolving a significant issue, or finishing a sprint/iteration.

**What's affected:** ADRs, standards, potentially solution docs.

**Guidance:**

- Have the agent review what was built versus what was documented.
- If decisions were made during implementation that aren't captured (technology choices, pattern departures, trade-offs), create ADRs.
- If recurring patterns emerged that should be formalised, update or create standards.
- If the implementation revealed that solution docs are stale or incomplete, update them.
- This prevents documentation drift — the longer you wait, the harder it is to reconstruct reasoning.

### New team member onboarding

**When:** Someone new joins the project.

**What's affected:** All areas (read-only).

**Guidance:**

- The new member (or their agent) reads `docs.index.md` as the entry point.
- Suggested reading order: `business-context.md` → `vision.md` → `outcomes.md` → `scope.md` → `solution-context.md` → `applications-context.md`. This gives them the "what and why" before the "how."
- For deeper orientation, have the agent summarise the current state of each area and highlight areas that are thin or flagged for enrichment.
- The business layer should be understandable without technical background. If it isn't, that's a signal the docs need improvement.

### Scope change or pivot

**When:** Business direction changes significantly — new priorities, dropped features, changed market, stakeholder realignment.

**What's affected:** `vision.md`, `outcomes.md`, `scope.md`, `assumptions-and-risks.md`, and cascade to solution.

**Guidance:**

- Have the agent read the current business docs and the new direction (meeting notes, revised brief, etc.).
- Update the business foundation first: scope, outcomes, and vision if needed.
- Then have the agent identify cascade impact: which solution docs, scenarios, and ADRs are affected by the change?
- Don't try to update everything at once — update business first, then solution, then standards if needed.

### Post-design-research synthesis

**When:** After completing user research (interviews, observations, usability tests).

**What's affected:** Personas, journeys, scenarios, potentially `business-context.md` and `assumptions-and-risks.md`.

**Guidance:**

- Place research outputs (interview notes, synthesis boards, insight statements) into a scratch folder.
- Have the agent create or enrich persona files from research findings — pain points, quotes, decision authority.
- Derive or refine journeys from observed workflows. Derive scenarios from journey steps.
- Update `assumptions-and-risks.md` with validated/invalidated assumptions from research.
- If using Design Thinking methods, see the DT mapping table in `docs.bootstrap.md`.

## Role guidance

**Software Engineers** — Primary engagement is with Solution, Standards, and Decisions. Use the structure to plan features against existing architecture, ensure consistency with standards, and capture decisions as ADRs. After implementation, reflect and update docs to prevent drift.

**Programme Managers / TPMs** — Primary engagement is with Business. Envisioning and kickoff outputs land in `business-context.md`, `vision.md`, `outcomes.md`, and `scope.md`. Use the business layer to maintain visibility of intent and track scope changes. The business layer should always be readable by non-technical stakeholders.

**Designers** — Primary engagement is with the Business layer's people-focused docs: personas, journeys, and scenarios. Design thinking outputs (interviews, synthesis, prototyping discoveries) feed directly into these files. The business layer is designed to be a first-class home for user-centred design artifacts.

**Data Scientists** — Personas and journeys provide grounding for evaluations and experiment design. Research findings land in the appropriate area — ML model decisions as ADRs, data quality constraints as assumptions, evaluation criteria linked to business outcomes.

## Tips and patterns

- **Use a scratch folder for raw inputs.** Meeting notes, exported documents, workshop photos — put them in `agent-temp/` or similar. These stay outside the canonical `docs/` structure. "Scratch pads stay out. Canonical knowledge comes in."
- **Always point the agent at `docs.bootstrap.md` first.** When starting any new documentation session, having the agent read the bootstrap and relevant framework files ensures it understands the structure before making changes.
- **Start with Phase 1 even on existing projects.** Anchor the business context (WHY) before diving into solution (WHAT). This prevents the common failure mode of building a well-documented solution that doesn't connect back to business intent.
- **Placeholder files are better than missing files.** A `vision.md` with two sentences and a "to be enriched" note is more valuable than no file at all — it signals that the area exists and needs attention. The agent can use it as an anchor for future enrichment.
- **Documentation is a living artifact.** These are not documents you write once and file away. They evolve as the project evolves. The lifecycle events in this playbook are recurring — you'll run many of them multiple times.
