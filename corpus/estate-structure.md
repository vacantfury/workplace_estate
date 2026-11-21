# Estate structure — shared conventions across the projects

*Estate-wide structural conventions every project shares (design principle 20d), ported selectively from the maintainer's broader working practice. Selection criterion: what makes an estate cumulative and self-correcting, carried as know-how only (principle 2: no machinery the seed cannot ship). Estate-wide law like the craft modules: consumed by every project, a project itself never.*

## The merged attention view (hub)

The hub can answer "what needs the user now" across the whole estate: one merged, ranked read over every project's TODO (due and active lanes) plus the standing due lanes (compensation windows, people threads, review cycles, health follow-ups). Rules:

- **Pull on ask, never push.** The view renders when the user asks; no per-project list auto-pops, no unsolicited digest.
- **The user's spoken priorities become pins.** When the user names something first or urgent, it pins above the computed order until done or unpinned; conversation is the one ordering channel.
- Convention first: a hub session computes the view by reading. An agent job may materialize it later; the job changes the labor, never the rules.

## Campaigns — the mid-scale ending form

Work larger than a task but smaller than a standing project (an org-networking push, an enrollment arc, a promotion push) runs as a **campaign**: one folder in the owning project, with `campaign.md` as the state file carrying a NAMED end, a small roster (pointers to cards/entries, never copies), an append-only move log, and exit criteria. The container never competes for attention; its individual moves ride the ordinary TODO. A campaign ends by DECISION: the closing pass records outcome against the named end plus lessons, and puts extend/close to the user explicitly. A silent lapse is a defect.

## Playbooks — the standing conditional form

A standing conditional program — do WHAT under WHAT condition, while a scope holds — runs as a **playbook**: one folder in the owning project, with `playbook.md` as the front door (named target · scope "while …" · state block `mode: steady | event-<branch> | retired` · log) and condition-headed **plays**, each an ordered set of steps. Campaign : move :: playbook : play — a play may spawn a campaign (passing a named end and a return path); a campaign never contains a playbook. The founding bar is deliberately high and the form RARE, ALL of: standing scope · a trigger that recurs or fires unpredictably · state remembered across firings · irreducible to one task line or standing rule · asymmetric cost of firing late or wrong. Below the bar the thing stays a register entry, a watch line, or a rule — the risk register's reaction plans (`risk-register.md`) are the lightweight kin, and a reaction plan that outgrows its entry (several condition branches, state across firings) promotes here. Every trigger is labeled honestly: observer (machine-observable · user-eyes-required · cadence-check) and reliability (a FRAGILE trigger is named as one the estate cannot guarantee timely entry on). Event plays open with a no-regrets first block that never waits; where a play rests on external parameters (a policy, a deadline, a legal term), the play stores them source-cited with a checked date, and a stale-but-needed parameter is re-verified IN PARALLEL with the no-regrets block, never before it. Plays edit at settle only, never mid-firing — a firing touches the state block and log alone; the after-action review updates the play. Retirement is a DECIDED event with a successor disposition (none / rule / register entry / archived); a silent lapse is a defect. Boundary: employer incidents stay with the employer's incident process (§What is deliberately NOT ported) — this form serves the estate's own standing conditionals. Form template: `skeleton/hub/_forms/playbook.md`, listed beside campaigns in the owning project's catalog.

## Lessons and handbook — lazy-founded, per project

- **`lessons.md`** — founded at a project's first lesson: concrete incidents worth keeping, each as story · mechanism · the rule that prevents recurrence.
- **`handbook.md`** — founded at a project's first point: established practice points (the correct way, the wrong way, the better way), each with where it was learned.

Estate-wide items land in the hub's copies. These files are why the estate improves instead of re-deriving; a lesson that stays in a session transcript is a lesson lost.

## The law layer — how the estate keeps its own rules

The estate's binding conventions have ONE canonical home per rule: hub law (the adapted corpus modules) plus per-project instruction files that CITE hub law, never copy it — a rule stated in two places diverges silently, so any restatement declares its master. Delivery is tiered by read guarantee (`session-discipline.md`, three-tier attention): only rules that must constrain every turn ride the always-loaded file; the rest live behind pointers, read when their situation arises. If hub law outgrows one file, the mature form is one RECORD per rule — a typed header (kind: rule / copy-of-a-master / advisory heuristic · delivery: always / on-event · scope) over the current rule text — with the always-loaded file becoming a GENERATED view of the records: regenerated, never hand-edited; edits land on records. Maintenance either way: law text states the CURRENT rule only (history lives in version control), every rule names its consumer, and a superseded rule is swept the session its supersession settles (`audit-law` checks this).

- **The placement rule: what loads at start.** A rule loads at start only if it can apply to any reply or any act in any session. A rule for one kind of act lives in that act's skill or in the owning project's instruction file, and the always-loaded text keeps only its binding line or a one-line pointer to it. A session that meets the situation outside the skill still holds the binding line. This is a placement rule, never a size limit.
- **Rules by audience.** The rules every acting agent loads (gates, conduct, the rules for anything an agent writes: files, drafts, records) are kept apart from the rules only sessions that talk with the user load (reply style, counsel, how steps are handed to the user). A headless job loads only the first set. The cut is by rule, not by file: a rule belongs to the first set when an agent that never talks with the user could break it by acting, building or writing; in doubt, it goes to the first set, since a rule wrongly kept in the second is missed by the agents that need it.

## The failures log and the self-audit

- **One estate failures log** (hub, `local/state/failures.md`): a dated row per real failure: what happened · cause side (instruction gap / verification gap / tooling / process / packaging) · level (the loss levels below). A person's error under absent or incomplete instruction attributes to the system, never the person (`session-discipline.md` completeness rule).
- **Loss levels.** A found problem's level is asked of that one problem, never of a project or a kind of check: "what does the user lose if this stays broken?"

  | Level | What the user loses |
  |---|---|
  | Critical | money, work or data lost for good; a dated obligation missed; something wrong sent to a person; a secret or employer-confidential content exposed |
  | Major | something the user ordered or relies on stops working |
  | Time | the user's hours (repeating, correcting, waiting) |
  | None | nothing anyone would notice |
  | Unknown | in doubt; stays visible, never counted as None and never higher |

  Inside a level there is no score, only an order: happening now first, then how often, then whether anyone would notice.
- **The self-audit runs only when the user starts it in a session.** It is never a standing job, a scheduled run or an unattended check. The fixes it finds are made in that same session. A session that meets a symptom may offer an audit once; it never starts one by itself.
- **It starts from clues.** A failure is an incident and stays where its project keeps it (this log, its task list). A clue is a sign, found by a fixed rule written in advance, that a project's own handling of its failures is not working. The rules read the failures log, the task lists and the job markers (`marker` and `silence_h`, `hub/agent-jobs.yaml`). In audit order:
  1. **Data lost:** a record or file that should exist is gone.
  2. **Found by the user:** a correction from the user whose cause no open ticket holds, signalled on more than one day.
  3. **Came back after a fix:** failures of a cause after its ticket closed.
  4. **Repeats unchanged:** the same failure recurring with no change, fix attempts included.
  5. **Claim contradicted:** a recorded claim (done, working, unavailable) that the live records contradict.
  6. **Due but silent:** a job past its silence window; a dated item passed with nothing done.

  Rules 1, 5 and 6 take direct proof: one lost record, one contradicted claim or one missed dated item is a clue on first sight. Rules 2, 3 and 4 need recurrence: for them one failure alone is never a clue, since a problem is found from the trend and recurrence of incidents (ITIL problem management), by conditions written before the incident (SRE postmortem triggers). Not clues under any rule: a first failure whose ticket is being worked, a failure that cleared by itself, a guard that refused correctly.
- **Clue records.** A rule that cannot read its record answers `unavailable` with the reason; no rule approximates (`agent-reliability.md`, unavailable, never fine). A clue's identity is its rule plus its key. A clue seen again keeps its first day; it is gone when its rule reads and no longer sees it; a rule that could not read leaves its clues exactly as they were. Records hold pointers (ids, paths, comparison facts), never copied source text.
- **One look per subject.** All open clues that share a subject get one judgment look: follow the records to the broken thing and its cause, decide whether it is a real defect, and quote every record relied on (`agent-reliability.md`, quote confirmation). A confirmed defect gets its loss level; one with an unconfirmed quote, or a look that cannot tell, is Unknown; a look that finds no defect marks its clues looked. A clue that had its look gets no second one; a new rule on the same subject makes a new clue. Looks go in rule order, then by signal count, then by age.
- **Treatment by level.** Critical and Major become a ticket in the owning project's task list (`task-convention.md` §Tickets), worked in the session. For an audit finding the check is the problem itself (its rule plus key), so each confirmed problem is its own ticket: importance urgent for Critical, important for Major, closed when the rule that found it runs again and no longer sees it. Time gets no ticket and is shown to the session that next changes that thing. None is a record only. Unknown stays visible and is not worked. The fixes are made under each project's own rules; behavior-changing ones wait for the user's word. Only work with a named gate (the user's word, a date or event the user named, an outside wait) is filed for later.
- **Gone only when unseen.** A problem is gone only when the rule or check that found it runs again and no longer sees it. A patch never closes it, and a recurrence reopens it.
- **The yield per rule.** Each run records, per rule: clues new, still open and gone; looks run; answers yes, no and unknown. A rule whose looks keep answering no goes to the user for revision. Renaming a rule or changing how its key is built moves its stored records in the same change. A rule is retired with a reason, never deleted, so its stored findings still resolve.
- **No audit without a clue.** Audits of things no clue points at are not run. They return to discussion only when clue runs stop finding new kinds of problems: the share of problem kinds seen only once falls (STADS saturation, Boehme 2018).
- **Loss tally, on the user's ask.** A read-only count over a window of what cost the user, by kind: the user's time, blocked runs, wasted fix attempts, lost work, open protections, and a residual other that is never dropped. Shares are compared within a kind, never across kinds. An unreadable source leaves its kind unavailable.
- **Backup verified, estate-wide:** the self-audit checks the WHOLE estate's backup against the A6 answer (`UNFOLD.md`): every project's state covered by the chosen route, and the route proved by the restore drill (`store.md`) and its receipt (a backup no drill has restored is unverified). The store's health line (`store.md`) is one input to this check, never the whole of it. A drill older than its window, or an A6 still unresolved, is a due-but-silent clue at the next self-audit, so conscious single-copy never becomes silent single-copy.

## Kinds and the dependency rule

The estate's containers have KINDS: the steward (hub) · infrastructure (store, finder, ties, llm_utils, devices, autoflow, auto_research) · function projects (worklog, compensation, career, health, risk, research) · the main-work manager with its per-project homes · plus the seed's registry row (kind: seed). Dependencies point ONE way: projects ride the infrastructure seams; infrastructure executes and never owns a project's meaning (scoring configs, dig briefs, triage semantics belong to the owning project). A capability two projects both need is infrastructure debt — flag it, never hand-roll it twice.

**The registry is a GRAPH:** every row also declares its EDGES — `consumes:` (which infrastructure seams) and `feeds:` (where its outputs flow, e.g. the company watch → career) — so the hub holds the whole estate's structure and renders it on ask.

**The crossing protocol** — state crosses a project boundary ONLY as one of four forms: ① a typed store entity under a declared schema (the wire format) · ② a dispatch line into the target project's TODO · ③ the hub's attention view / task head · ④ a declared engine job naming source → target. A direct write into another project's state files is a defect.

- **Links go by stable name.** A link from one project's record to another project's entity goes by the target's stable name (its slug; for a work item, its project plus its never-reused id), never a storage row id, and is declared beside the referring project's schema. A read-only check lists links that resolve to nothing. The referenced side never makes a key vanish silently: a merge leaves a redirect, and retiring a key is refused while any link still points in. A catalog of what the stores actually hold shows an undeclared table as unknown, never as link-free.
- **Form ① carries facts only.** A typed store entity crossing a boundary refuses unknown fields and other schema versions, and refuses meaning fields by name (verdict, score, rank, priority, outcome, decision and the like). Each project adds its own judgment fields locally, and scores travel as the owning project's own assessments in the store (`store.md`), never as fields of the crossing entity. Each project's `schemas.yaml` carries its `schema_version`: an added field is a minor schema change; a removed or retyped field bumps the version, and a consumer accepts only the versions it declares.

## The concrete tree — structure ships as files, not prose

The estate's default directory layout is SHIPPED, not described: the seed's `skeleton/` directory is the installed estate's concrete form — one directory per roster project, every state file present as a template with its header, sections, and config block already written, the registry (`hub/registry.yaml`) and job registry (`hub/agent-jobs.yaml`) as real schema files. The tree is drawn once in `skeleton/README.md`; corpus references to a project's own `local/state/<file>` resolve to it via the registry TODAY. **Target layout (`store.md` §The engine is resolved at unfold, "Where the engine's data lives"):** once the store engine lands, that data moves OUTSIDE the project folders into one data home, one folder per project — `store` and `state` never naming a folder inside a project again. That move rides the store engine's own rollout (A7), not a per-reference rewrite of this section. The split is deliberate: conventions are GENOMES (prose, adaptive — team reality wins); structure is PHENOTYPE (deterministic — the unfold copies, then adapts, and never invents layout). A structural change to the estate is therefore a skeleton change in the seed, shipped as a versioned delta, never a per-install improvisation.

## The data-shape rule

Any register that scores or types its entries (the compensation register, career's theme register) follows one shape:

1. **Typed entries** with named fields, not free prose.
2. **Append-only dated assessments** carrying their evidence; corrections are new lines, never edits of old ones.
3. **Machine estimates separate from the user's own judgments** — labeled, and the user's layer never overwritten.
4. **Weights, thresholds, and cadences in a config block**, tunable, never buried in prose or code.

Markdown registers are fine at estate scale; the shape matters, not the storage engine. If a register ever outgrows markdown, the shape migrates unchanged into whatever store the sanctioned tooling offers — the store service (`store.md`) owns that engine and that migration.

## The placement map — where kinds of things live

Every KIND of content the work produces has one named home, and the user never memorizes the mapping: they ask, the hub answers (design principle 23). The hub's estate registry carries a placement table — content kind → home: team docs in the team's canonical doc system · code in the employer's git · the estate's own records per the project registry · meeting artifacts with their owning project · scratch and downloads in one named scratch spot, cleaned periodically. The real surfaces are discovered at intake (`knowledge/week1-intake.md` §21): the team's actual storage practice and what the policy sanctions win over any default. A new content kind that settles gets its row the same session; a file with no home row is misfiled by definition.

## Forecast lines — predictions that resolve

Any register may carry dated RESOLVABLE predictions: `forecast: <claim> · resolve by <date or event> · likelihood <band>`. When the date or event arrives, the line is resolved against what actually happened, never quietly dropped. On the user's ask, a calibration read takes resolved lines as a calibration record (hit rate by band); it is a procedure the user starts, never part of a clue run and never scheduled. It reads alongside the risk register's predicted-vs-unpredicted check (its failure-side half). Typical writers: the company watch (will this theme get resourced; will this reorg land) · the portfolio board (will this project reach its declared end at its planned scale) · the performance project (cycle-outcome expectations). The point is compounding judgment: a prediction with no resolution discipline teaches nothing.

## What is deliberately NOT ported

Heavier structure stays out until a real work-side consumer exists: no standing multi-agent deliberation INFRASTRUCTURE (the deliberation convention itself is in — `deliberation.md`, know-how run inside the sanctioned tooling), no version-tagged releases (the SEED ships no software; what the founded estate builds is its own affair), no databases or OS-level schedulers BESIDE the sanctioned tooling (the automation platform — `autoflow.md` — runs THROUGH the sanctioned tooling, never beside it), no external-feed collection (design principle 12), and no message-transport machinery of its own (the people/message/meeting flow convention is in — `ties.md` — run entirely on the employer's directory, mail, chat, and calendar surfaces). Infrastructure IS ported, sized to the known end-state (design principle 25): the store (`store.md`, typed data + scoring service), the finder (`finder.md`, one retrieval seam over the job's channels), and the work-stack quartet — `llm_utils.md` (LLM provider seam) · `devices.md` (compute and device client) · `autoflow.md` (automation platform) · `auto_research.md` (autonomous research engine) — each founding at its named consumer gate (user decisions 2026-08-24; the quartet supersedes its earlier absorption into module prose; incumbents sit BEHIND these seams, never replace them). Also absent by decision: no aid-portfolio system (helping colleagues and mentees runs as people-project campaigns), and no urgency-runbook system (the employer's incident process governs; personal quick-reaction prep lands as role-playbook notes only where the team leaves a gap).

## Fold-away note (for the unfold's A5 pass)

Core-adopt: each convention costs at most a file. On a degraded (no-agent) install, the attention view becomes a session-opening read and the self-audit stays a procedure the user starts; everything else is unchanged.
