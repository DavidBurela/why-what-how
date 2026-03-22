# Repository Guidance

## What this repo contains

The `docs/` folder contains project-agnostic framework guidance files for the Why–What–How engagement knowledge model. These files are designed to be copied into project repositories as a starting point.

The files in `docs/` are **not** a project instance — they are the framework definition itself: the core model, conventions, folder structure, bootstrap playbook, and area-specific guidance.

## How to navigate

Start at `docs/docs.index.md` — it is the entry point and navigation router.

Load context progressively by depth, not all at once:

1. `docs/docs.index.md` — overview and links to all framework files
2. `docs/docs.why-what-how.md` — the core four-area model (Business, Solution, Standards, Decisions)
3. Load specific files as needed:
   - `docs/docs.why-what-how.area-guidance.md` — what sections to write in each file type
   - `docs/docs.why-what-how.bdd.md` — behaviour stack (journeys, scenarios, BDD)
   - `docs/docs.why-what-how.c4model.md` — C4 model role and validation
   - `docs/docs.conventions.md` — naming, linking rules, ID patterns
   - `docs/docs.structure.md` — target folder tree and structural rules
   - `docs/docs.bootstrap.md` — phased creation playbook
