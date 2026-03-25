# Prompt Examples

Copy-paste-ready prompts for working with the Why–What–How framework using AI agents.

Each prompt is designed to be pasted directly into an agent session. Replace `{placeholders}` with your project-specific values. Prompts reference the framework guidance files — ensure your project has the `docs.*.md` files copied from the [Why–What–How core repository](https://github.com/DavidBurela/why-what-how).

For guidance on when to use each prompt and how it fits into the project lifecycle, see `docs/docs.playbook.md`.

> **Last reviewed:** 2026-03-25

## Quick reference

| Scenario | Prompt | Who |
|----------|--------|-----|
| **Getting started** | | |
| New project, early discussions | [Bootstrap a new project](#bootstrap-a-new-project) | Any |
| Existing project, restructure docs | [Refactor existing docs](#refactor-existing-docs-into-why–what–how) | Any |
| Existing project, non-disruptive tryout | [Distil alongside existing docs](#distil-into-why–what–how-alongside-existing-docs) | Any |
| **Business** | | |
| After a discovery or kickoff session | [Update business docs from session notes](#update-business-docs-from-session-notes) | TPM |
| After user research or DT workshops | [Create personas, journeys, and scenarios](#create-personas-journeys-and-scenarios-from-research) | Designer |
| **Solution** | | |
| After an architecture design session | [Update solution docs from architecture session](#update-solution-docs-from-architecture-session) | SE |
| External dependencies identified | [Define system context](#define-system-context-and-external-dependencies) | SE |
| Breaking down into deployable units | [Break down into applications](#break-down-into-applications) | SE |
| Structural diagrams needed | [Generate C4 model](#generate-c4-model-from-solution-docs) | SE |
| C4 model may have drifted | [Validate C4 model](#validate-c4-model-against-solution-docs) | SE |
| **Testing** | | |
| Scenarios ready for verification | [Create BDD feature file stubs](#create-bdd-feature-file-stubs-from-scenarios) | SE |
| **Implementation** | | |
| Planning a feature or backlog item | [Plan a feature](#plan-a-feature-against-existing-architecture-and-standards) | SE |
| After completing a feature | [Review and update docs](#review-implementation-and-update-documentation) | SE |
| **Lifecycle** | | |
| New team member joins | [Guided project orientation](#guided-project-orientation) | Any |
| Business direction changes | [Assess scope change impact](#assess-scope-change-impact) | TPM |
| After completing user research | [Synthesise design research](#synthesise-design-research-into-business-docs) | Designer |

## Bootstrap

### Bootstrap a new project

**When to use:** You're starting a new project — still in early discussions and envisioning — and want to start structuring the information you have.

**What to prepare:** Place all raw inputs (meeting notes, business problem docs, workshop outputs, background material) into a scratch folder (e.g. `agent-temp/`).

```text
Read `docs/docs.bootstrap.md` to understand the phased creation order, then read `docs/docs.conventions.md` for naming rules and `docs/docs.why-what-how.area-guidance.md` for expected file sections.

Then read all files in `{path-to-scratch-folder}` — these are raw inputs from discovery/envisioning sessions.

Make a plan for executing Phase 1 (Foundation) and Phase 2 (Who and Why) of the bootstrap:
- List the files you would create under `docs/business/`
- For each file, summarise what content you would extract from the raw inputs
- Flag any gaps where the raw inputs don't provide enough information

Present the plan for my review. After I approve, execute it — creating the files with real content extracted from the inputs, following the expected sections from `docs.why-what-how.area-guidance.md`.
```

### Refactor existing docs into Why–What–How

**When to use:** You're on an existing project with scattered markdown (ADRs, design docs, SDDs, research) and want to restructure into Why–What–How. This is the preferred path — it consolidates docs into the canonical structure, removes redundancy, and updates cross-references.

**What to prepare:** Ensure `docs.*.md` framework files are copied into your project. Know which folders contain existing documentation.

```text
Read `docs/docs.bootstrap.md` and `docs/docs.structure.md` to understand the target structure, then read `docs/docs.conventions.md` for naming rules.

Audit this repo's existing markdown documentation. For each markdown file outside `docs/`, determine:
- Which Why–What–How area it maps to (Business / Solution / Standards / Decisions)
- Whether it has a canonical home in the target structure
- Whether it overlaps or duplicates other files

Produce a refactoring plan:
1. What moves where (existing file → canonical location)
2. What files should be merged (duplicates or overlapping content)
3. What gaps need placeholder files (especially in the Business layer — existing repos typically have thin or missing personas, journeys, and scenarios)
4. What cross-references need updating after moves

For Business layer gaps, note what can be inferred from existing docs (stakeholders from ADRs, scope from design docs, etc.) and what requires new input.

Present the plan for my review. After I approve, execute incrementally — commit after each logical group so the history is traceable.
```

### Distil into Why–What–How alongside existing docs

**When to use:** Same scattered repo as above, but you want to try the structure without moving or disrupting existing files. Lower risk — good for evaluation before committing to a full refactoring. The downside is temporary duplication.

**What to prepare:** Same as refactor — ensure framework files are copied in.

```text
Read `docs/docs.bootstrap.md` and `docs/docs.structure.md` to understand the target structure.

Audit this repo's existing markdown documentation and map each file to a Why–What–How area (Business / Solution / Standards / Decisions).

Create the canonical `docs/` structure alongside the existing files — pull high-signal content into the new docs rather than moving the originals. This means:
- Create `docs/business/`, `docs/solution/`, etc. with proper files
- Extract and distil content from existing docs into the new structure
- Leave original files in place (they'll coexist temporarily)

Note: this creates duplication. Plan to either migrate fully or accept the redundancy. The benefit is low-risk evaluation of the structure before committing to full refactoring.

Present a plan before executing. Flag where content is thin and needs future enrichment.
```

## Business

### Update business docs from session notes

**When to use:** After a discovery session, envisioning workshop, stakeholder alignment meeting, or project kickoff. Relevant for TPMs and programme managers.

**What to prepare:** Place meeting notes or session outputs into a scratch folder.

```text
Read `docs/docs.why-what-how.area-guidance.md` for expected sections in business files.

Then read the existing business docs:
- `docs/business/business-context.md`
- `docs/business/vision.md`
- `docs/business/outcomes.md`
- `docs/business/scope.md`
- `docs/business/assumptions-and-risks.md` (if it exists)

Then read the new session notes in `{path-to-session-notes}`.

Compare the current docs against the new information. Propose specific updates:
- New content to add (with the exact sections where it belongs)
- Existing content that needs refinement or correction
- Contradictions between current docs and new inputs that need resolution
- New assumptions or risks surfaced by the session

Present proposals for my review before making changes. Flag anything that requires human judgement — envisioning outputs often contain nuance.
```

### Create personas, journeys, and scenarios from research

**When to use:** After completing user research, design thinking workshops, or stakeholder interviews. Relevant for designers and researchers.

**What to prepare:** Research outputs (interview notes, synthesis boards, insight statements) in a scratch folder.

```text
Read `docs/docs.why-what-how.area-guidance.md` for expected sections in persona, journey, and scenario files. Read `docs/docs.conventions.md` for naming conventions (JNY-xxx, SCN-xxx format).

Then read the research outputs in `{path-to-research-folder}`.

From the research findings:
1. **Personas** — create persona files under `docs/business/personas/`. Include: who they are, what they care about, what they want from this system, pain points, and key quotes from research. Update `personas.index.md`.
2. **Journeys** — derive journeys from observed workflows. Create journey files (JNY-xxx format) under `docs/business/journeys/`. Each journey: persona link, goal, trigger, numbered steps, success criteria. Update `journeys.index.md`.
3. **Scenarios** — extract testable behavioural slices from journey steps. Create scenario files (SCN-xxx format) under `docs/business/scenarios/`. Each scenario: Given/When/Then in business language, linked journeys. Update `scenarios.index.md`.

Link journeys to their derived scenarios, and scenarios back to their parent journeys. Present the plan before creating files.
```

## Solution

### Update solution docs from architecture session

**When to use:** After an architecture design session (ADS), system design review, or significant technical decision.

**What to prepare:** Place session notes and any diagrams/sketches into a scratch folder.

```text
Read `docs/docs.why-what-how.area-guidance.md` for expected sections in solution files, and `docs/docs.conventions.md` for ADR naming conventions.

Read the existing solution docs:
- `docs/solution/solution-context.md`
- `docs/solution/applications/applications-context.md`
- All application `app-context.md` files under `docs/solution/applications/`

Then read the architecture session notes in `{path-to-session-notes}`.

Compare existing solution docs against the session outputs. Focus on:
1. System boundary changes — has the boundary expanded or contracted?
2. New or removed applications — do any application folders need creating or marking as deprecated?
3. Changed relationships — have integration patterns or dependencies shifted?
4. New external dependencies — are there new external systems to add to `solution-context.md`?

For each significant choice made in the session, draft an ADR capturing the decision, alternatives considered, and trade-offs.

If the C4 model exists (`docs/solution/c4-model/workspace.dsl`), update it to reflect structural changes.

Present all proposed changes for my review before applying.
```

### Define system context and external dependencies

**When to use:** The team has identified what external systems the solution depends on or interacts with.

**What to prepare:** Know the external systems, their roles, and how the solution interacts with them.

```text
Read `docs/docs.why-what-how.area-guidance.md` for the expected sections in `solution-context.md`.

Read the existing `docs/solution/solution-context.md` if it exists.

The external systems for this solution are:
{list each external system with: name, what it does, direction (inbound/outbound/both), protocol/integration pattern}

Create or update `docs/solution/solution-context.md` with:
- System boundary narrative (what is inside vs outside)
- External systems table (system, role, integration pattern)
- Data flow summary if enough information is available

Define dependencies at the solution level. Application-specific details will be added when applications are defined.
```

### Break down into applications

**When to use:** Ready to decompose the solution into deployable units.

**What to prepare:** Initial thoughts on the applications (e.g. "a React web frontend, a .NET API, a PostgreSQL database").

```text
Read `docs/docs.structure.md` for folder conventions, `docs/docs.conventions.md` for naming rules, and `docs/docs.why-what-how.area-guidance.md` for application doc expected sections.

Read the existing solution docs under `docs/solution/`.

The initial application decomposition is:
{list each application with: name, technology, purpose, short code (e.g. API, WEB, WKR)}

For each application:
1. Create the folder `docs/solution/applications/{app-name}/`
2. Create `{app-name}.index.md` — navigation hub with links to app-context, source code path
3. Create `app-context.md` — what it is, technology, capabilities, dependencies

Then update:
- `docs/solution/applications/applications-context.md` with cross-application relationships
- `docs/solution/solution.index.md` with the applications table and initial scenario→flow traceability (use "—" for flows not yet written)
```

### Generate C4 model from solution docs

**When to use:** Solution structure is stable enough that structural diagrams would be valuable.

**What to prepare:** Populated solution docs (solution-context, applications, relationships).

```text
Read `docs/docs.why-what-how.c4model.md` for C4 model conventions.

Read all solution docs:
- `docs/solution/solution-context.md`
- `docs/solution/applications/applications-context.md`
- All application `app-context.md` files under `docs/solution/applications/`
- Any documented flows

Generate `docs/solution/c4-model/workspace.dsl` with:
- System context view (solution boundary, external systems, users)
- Container view (applications and their relationships)
- Dynamic views for any documented flows
```

### Validate C4 model against solution docs

**When to use:** Periodic check when solution docs may have drifted from the C4 model, or before a milestone/review.

**What to prepare:** Existing C4 model and solution docs.

```text
Read `docs/docs.why-what-how.c4model.md` for C4 conventions.

Compare the C4 model (`docs/solution/c4-model/workspace.dsl`) against the solution markdown docs:
- Are all applications in solution docs represented in the model?
- Are all relationships consistent between the model and the markdown?
- Are dynamic views current with documented flows?
- Are there elements in the model that no longer exist in the docs?

Report discrepancies as a table: element/relationship, what the model says, what the docs say, which to update. Fix in whichever direction is more current.
```

## Testing

### Create BDD feature file stubs from scenarios

**When to use:** Scenarios are documented and the team wants executable verification placeholders. These start red (failing) and turn green as implementation progresses.

**What to prepare:** Documented scenarios in `docs/business/scenarios/`.

```text
Read `docs/docs.why-what-how.bdd.md` for BDD conventions.

Read all scenario files under `docs/business/scenarios/`.

For each scenario, create a BDD feature file stub:
- Location: `{path-to-test-folder}` (application test folder, NOT under `docs/`)
- One feature file per scenario
- Given/When/Then skeleton using business language only — no HTTP verbs, no JSON, no API paths
- Reference the scenario ID via tags (e.g. @SCN-001)
- Include placeholder step definitions if the test framework requires them

After creating the feature files, update each scenario file with a navigable link to its corresponding feature file.

These stubs start failing. The team turns them green during implementation.
```

## Implementation

### Plan a feature against existing architecture and standards

**When to use:** A developer is preparing to implement a feature, backlog item, or SDD spec.

**What to prepare:** Know which application and feature you're implementing.

```text
Read the application docs at `docs/solution/applications/{application}/` (especially `app-context.md`) and the standards at `docs/standards/`.

The feature I'm implementing: {brief description of the feature or backlog item}

Based on the existing architecture and standards:
1. Propose an implementation approach that's consistent with established patterns
2. Identify which standards apply to this work
3. Flag where new flows, ADRs, or standard updates may be needed
4. Note any potential conflicts with existing architecture decisions

This is a planning step — catching misalignment before coding starts.
```

### Review implementation and update documentation

**When to use:** After completing a feature or resolving a significant issue. Prevents documentation drift by capturing reasoning while it's fresh.

**What to prepare:** Know what was built and any decisions made during implementation.

```text
Read the relevant solution docs under `docs/solution/applications/{application}/`, recent ADRs in `docs/decisions/`, and standards in `docs/standards/`.

Here's what was built: {description of what was implemented, any notable decisions or trade-offs made during implementation}

Review and recommend:
1. **ADRs** — Were any decisions made during implementation that aren't captured? (technology choices, pattern departures, trade-offs) If so, draft them.
2. **Standards** — Did recurring patterns emerge that should be formalised? Propose updates.
3. **Solution docs** — Are any existing docs now stale or incomplete given what was built? Flag them with specific corrections.
4. **Scenarios/flows** — Does the implementation support scenarios that aren't yet documented, or change how existing flows work?

Present recommendations for my review.
```

## Onboarding

### Guided project orientation

**When to use:** A new team member joins and wants to understand the project. Also useful for testing documentation quality — if the agent can't produce a coherent briefing, the docs need improvement.

**What to prepare:** Nothing — the docs should be self-orienting.

```text
Read `docs/docs.index.md` as the entry point. Follow the navigation structure to read the key docs.

Produce a structured project briefing for a new team member:

1. **Business context** — What problem does this solve? Who are the key personas? What are the success criteria?
2. **Solution architecture** — What are the main applications? How do they connect? What external systems are involved?
3. **Key decisions** — What significant architectural or technology choices were made, and why?
4. **Standards** — What conventions and patterns does the team follow?
5. **Current state** — Which areas of the documentation are well-developed? Which are thin or flagged for enrichment?

Suggested reading order for deeper understanding:
business-context.md → vision.md → outcomes.md → scope.md → solution-context.md → applications-context.md

Present the briefing in a format suitable for sharing with the new team member.
```

## Scope change

### Assess scope change impact

**When to use:** Business direction changes significantly — new priorities, dropped features, changed market, stakeholder realignment. Relevant for TPMs.

**What to prepare:** Place notes on the new direction (meeting notes, revised brief, etc.) into a scratch folder.

```text
Read the current business docs:
- `docs/business/business-context.md`
- `docs/business/vision.md`
- `docs/business/outcomes.md`
- `docs/business/scope.md`
- `docs/business/assumptions-and-risks.md`

Then read the new direction at `{path-to-scope-change-notes}`.

Assess the impact:
1. **Business foundation** — What changes in scope, outcomes, and vision? Draft the specific updates.
2. **Cascade to solution** — Which solution docs, applications, and relationships are affected?
3. **Cascade to scenarios** — Which scenarios are invalidated, need revision, or are newly required?
4. **Cascade to decisions** — Which ADRs may need superseding or revisiting?

Update business docs first. Present the cascade impact assessment for solution and decisions before making those changes.
```

## Design research

### Synthesise design research into business docs

**When to use:** After completing user research (interviews, observations, usability tests). Relevant for designers.

**What to prepare:** Research outputs (interview notes, synthesis boards, insight statements) in a scratch folder.

```text
Read `docs/docs.why-what-how.area-guidance.md` for expected sections in persona, journey, and scenario files.

Read existing business docs:
- `docs/business/personas/` (all persona files)
- `docs/business/journeys/` (all journey files)
- `docs/business/scenarios/` (all scenario files)
- `docs/business/assumptions-and-risks.md` (if it exists)

Then read the research outputs in `{path-to-research-folder}`.

From the research findings:
1. **Enrich personas** — add pain points, key quotes, and decision authority from interviews
2. **Refine journeys** — update journey steps based on observed workflows; create new journeys if research reveals paths not yet captured
3. **Derive scenarios** — extract new testable behavioural slices from updated journeys
4. **Update assumptions** — mark assumptions as validated or invalidated based on research evidence; add new assumptions surfaced by the research

Present changes for review before applying. Flag where research contradicts existing documentation.
```
