# Store — the estate's typed data service

*One shared typed store + scoring service that every register rides (design principle 25). The data-shape rule (`estate-structure.md`) is this service's CONTRACT; this module is the ENGINE that enforces it. Consumers: the resources register, the company signal and theme registers, the worklog's structured lines, per-project boards, and the task lists (store-backed form, `task-convention.md`) — any register that types or scores its entries.*

## The service

- **The store keeps the generic tables; each project owns its vocabulary.** The store provides five generic tables: `entities`, `assessments` (append-only and evidenced, machine rows split from the user's own), `relations`, `events` and `candidates` (the intake inbox, below), and it executes scoring. Each project owns its entity kinds, what their fields mean, and its weights and bands, in a `schemas.yaml` in its own project folder: the hub's holds the task model and the self-audit rows, career's the `signal`, `theme` and `event` kinds, compensation's the `resource` kind. The store's own `schemas/schemas.yaml` declares only the generic tables. Each kind's schema names its fields and which are machine-computed versus the user's own judgment; registers never invent ad-hoc shapes.
- **One truth database per project.** No database spans projects. Another tool's database stays its own file beside the truth database (below). A project opens a second store file only for a part with its own writer or its own lifecycle that references nothing in the first. A reference from one project's data to another's follows the crossing protocol (`estate-structure.md`).
- **Scoring runs in the store; meaning stays with the owning project.** A register's scoring config (weights, thresholds, bands — the data-shape rule's config block) is authored by the owning project; the store executes it uniformly and stamps every score with config version, date, and an evidence pointer.
- **Append-only assessments; the user's judgment layer is never overwritten** (data-shape rule points 2–3).
- **Every assessment carries a direction and two times.** Direction is `supports`, `disputes` or `neutral`: a confidence number alone cannot tell weak evidence for a value from evidence against it. The two times are the SQL:2011 split between valid time and transaction time: **valid time** is when the assessed thing was true, stated by the caller, and every decay runs on it; **recorded time** is when the row was written, stamped by the store's own clock and never the caller's, so the write trail cannot be back-dated. Each row also carries its source (machine or user), confidence, evidence pointer and config version.
- **Four scoring folds** (ported from proven closed forms; every knob — weights, priors, half-lives, band edges — lives in the CONSUMING project's config): **estimate** — a latent quality inferred from noisy evidence as a Bayesian normal-conjugate posterior (confidence maps to precision, old evidence decays by half-life; mean ± sigma out — for person reception, event value, theme strength); **balance** — a decay-weighted signed event account, deliberately no Bayes (quiet stretches drain it — for relationship investment, momentum); **forecast** — a resolvable claim revised by explicit Bayesian odds arithmetic (both likelihoods stated and contestable; scored by Brier against the world — the estate's forecast lines); **bands** — the score→label mapping. Pick the fold by the question's shape; a register never invents its own arithmetic.
- **The folds read direction.** **balance** negates a disputing row (a debit against the account). **estimate** enters a disputing row reflected about the prior mean, at unchanged precision: direction says which way, confidence says how hard. **forecast** reads its own likelihood pair, which already states which way an update cuts. A `neutral` row is kept for the record and adds nothing to the arithmetic: no value, no weight, no count.
- **Views, not copies.** Once the store runs, the markdown files sessions read (`compensation.md`, `themes.md`, …) are RENDERED views; a hand edit to a view that carries judgment flows back as a new user-layer line, never silent divergence.
- **The engine is resolved at unfold (A7):** the best sanctioned storage engine the device offers — an embedded database where a runtime exists (SQLite-class), the tooling's native memory otherwise. Markdown-with-shape is the bootstrap form; migration is the data-shape rule's own line: the shape moves unchanged, the store owns the move.
- **Where the engine's data lives, once it lands:** one data home OUTSIDE the project folders, one folder per project — `data/<project>/`, holding that project's truth database (everything its own code creates), any other tool's database as its own file beside it (checkpoints, a cost ledger, tuning trials — each tool keeps its own file and its own migrations, never inside the truth database), found-data `inputs/`, and a deletable, regenerable `cache/`. Code and rendered views stay in the project folders; only data crosses into the data home. **Naming rule:** a project folder is data/state-free — `store` and `state` never name a folder INSIDE a project again; `data/` inside the data home is the only home data ever gets.

## Data declarations

- **Declare before writing.** Each project declares every store it writes before the store's first write, in `<project>/stores.yaml` in its project folder. Per store: its **kind** (a truth database, another tool's database, found inputs, a cache, a folder of files); its **keep class**: `unique` (the only copy of something that cannot be made again), `unknown`, `reproducible` (can be rebuilt; the declaration names its **regeneration source**) or `disposable`; its **retention** (after what, and kept for how long); and a **permission for each operation** (compress, retire, archive, move), each `forbidden`, `automatic` or `user-press`.
- **Doubt keeps data.** A store with no declaration reads as `unknown` and is kept. In doubt, data counts as `unique`. The employer's data-retention policy wins over any declared retention.
- **Copies are declared too.** Each copy of a store (taken before a change, for an audit, as evidence) is recorded in the copy ledger under a class that states its purpose and the reason for its keep rule. A **pin** holds a copy while a finding or decision relies on it, and records which one. **Prune** is a dry run by default; an apply rechecks each copy's size, identity and hash before removing it, and pruning is disabled while any class, any reason or the copy ledger itself is unreadable.
- **When the form lands.** The form `hub/_forms/stores.yaml` is instantiated as `<project>/stores.yaml` at the project's first store in the data home. Until then, every markdown state file counts as `unique`.

## Intake with recorded drops

- **One lifecycle.** An intake candidate (a found item handed to a project for its judgment) moves `received`, then `judged`, then `accepted` or `dropped`. Each move is a recorded event on the candidate.
- **A drop is a record.** A drop needs a reason and a reopen condition. A re-handoff of the same item never revives it; reopen is the only way back, and it names what fired.
- **The producer's score is evidence, never the verdict.** The score a candidate arrives with is one machine assessment on it; the verdict is the consuming project's, held in the lifecycle state.
- **Duplicates fold.** Duplicates fold into the record furthest along. The other is dropped as a duplicate, and the fold can be undone (unfolded).
- **Missed items are checked by sample.** A seeded random sample of drops is read back, read-only, as the check for items dropped that should have gone on.
- **Intake follows the finder's boundary** (`finder.md`): employer surfaces plus the public retrieval the environment itself sanctions, never unsanctioned feeds.

## Archive before delete

- **Finished rows or files leave a live store only into a read-only archive.** The archive is read back equal (digests match) before anything is deleted, and the receipt of that readback is recorded in the same transaction as the delete.
- **What stays.** Anything still referenced, or newer than a grace age (set in the store's declared retention), stays in the live store.
- **Room first.** A free-disk reserve check runs before the archive is written; short of the reserve, nothing is written and nothing is deleted.
- **The producing project decides what is finished**, never the store.

## Backups and the restore drill

- **A database is never backed up by a plain copy of a live file** (it can capture a half-written page). It goes through a consistent snapshot or the engine's online backup, passes an integrity check, and lands by atomic rename. A file that cannot be copied keeps its previous copy and is named in the run's failure list; the other files still copy.
- **What a backup leaves out:** `cache/` and what the declarations call `disposable`. An unreadable declaration leaves nothing out.
- **The restore drill.** Restore the backup into a scratch location, check every database (integrity) and every file, and record a receipt: the date, what was restored, and what each check found. The drill recurs at a cadence the user confirms (the optional restore-drill entry in `hub/agent-jobs.yaml`). A drill older than its window is a clue for the next self-audit (`estate-structure.md`).
- **Restoring one project to an earlier point** names the window of writes it loses. Dropping them is the user's call.

## Engine-side write safety

*Applies once a database engine runs (A7); the markdown form carries none of this.*

- **Operation ids.** A write may carry an operation id. A retry with the same id replays the recorded result without repeating the write; the same id with different content is refused. Bulk writes run at one or two workers with an id per item, so a resumed batch is safe.
- **A cross-project write is one envelope.** It is staged as one versioned envelope with a stable operation id, inside the writer's own transaction, and is answered `applied`, `refused` or `queued`. Refusal codes are a closed list, each with a class: `final` (ended for this id), `fence` (ended on a stale fence; judged again when the same envelope is sent again) or `held` (not decided; answered `queued`). The residual `unknown` counts as `final`, so an unclassified refusal reaches attention instead of looping. An error that decided nothing answers `queued` with outcome unknown, never `refused`.
- **The store records its format.** A writable open by an older writer refuses a newer format; read-only opens are allowed. A change an older writer could corrupt bumps the format.
- **Two locks.** A long-running writer holds a shared writer lock for its run, and an offline migration takes it exclusive. This lock is separate from the short maintenance lock, so a writer never blocks backup or retention.
- **Snapshots for runs.** A run that needs live store data takes a verified read-only snapshot under a named holder and releases it when done. A copy of a live store never sits in a working copy or an undeclared folder.
- **A report that always answers.** A read-only report lists every database in the data home from schema metadata and always succeeds; a locked file reports `busy`.

## Standing jobs (registry entries, `work-engine.md`)

- **Schema keeper** — a new entity kind lands as a schema entry first; drift between a register and its schema is flagged, never silently absorbed.
- **Scoring runs** — recompute machine scores on the owning project's cadence; a delta surfaces through the hub attention view only when it changes a decision lane.
- **Store health:** backup per A6, by the method above. Row counts, staleness and the last restore drill's receipt are read when the user runs the self-audit (`estate-structure.md`).
- **Hand-run writes:** a write a session makes by hand to a live store follows the `live-store-write` skill (`portable-skills.md`).

## Fold-away note (for the unfold's A5 pass)

Core-adopt the CONTRACT at every outcome (the data-shape rule already binds); the ENGINE lands when A7 finds a sanctioned store. Degraded install: markdown registers keep the shape, scoring is a session pass.
