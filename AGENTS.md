# CLAUDE.md

**Visibility: public** (flipped from private 2026-08-06, after a clean full-history scan): public so the SEED channel is credential-free — clone and pull need no authentication on the work device. (The original stronger claim — no personal credential ever touches the corp machine — was superseded 2026-08-15 by the graded-boundary ruling, design principle 17: the user's own credentials may land in revocable per-device, footprint-registered form; see `corpus/boundary-protocol.md` credential rule.) Committed content was held to **public-grade discipline from birth** by hard rule: the clone target is an employer-managed machine, so everything committed is written as employer-readable — no personal data, no secrets or secret-manager references, no private-system internals. Founded 2026-08-03, entirely before the maintainer's employment start date: all content is the author's own work, authored on personal equipment with clean provenance.

## What this repo is

An **open work tool**, shaped as an installation package: a portable working-conventions toolkit for operating well on an employer-managed work device. The committed repo stays permanently generic; it is cloned onto a work device, where its unfold procedure detects the environment (work docs + device) and FOUNDS the work-side ESTATE — a copy of the shipped `skeleton/` tree, adapted: hub · store · finder · ties · worklog · compensation · career · health · risk · research · main-work with its per-project homes, plus gated infrastructure (llm_utils · devices · autoflow · auto_research) — the same estate structure the user works in anywhere, restricted to work-relevant parts and extended with work-native ones (design principles 19–20, 25–30) — all machine-local, never pushed back. It contains ONLY:

- the corpus: portable working discipline a work environment may use — task convention, session working style, engineering standards, generically useful skills;
- idea/direction notes about how to structure work-machine workflows;
- `UNFOLD.md`, the installer procedure.

**On a work machine, the first session's duty is to run `UNFOLD.md`.** Full model: `text_docs/design.md`.

## Scope boundary (load-bearing)

**This repo owns:** portable working discipline safe for a corporate device — e.g. the ordered-TODO task convention, engineering standards (uv, parameters-in-config-not-code), session discipline.

**Never enters this repo:** personal data of any user's, anything derived from any employer, and knowledge about how any particular user relates this tool to the rest of their life — the tool describes only itself.

**The division, one line (settled 2026-08-06):** this installation = the job (day-to-day operations inside the employer boundary) · the employment's wider meaning for the user's life is their own affair beyond it. The installation is self-contained; boundary discipline (`corpus/boundary-protocol.md`) binds: employer-confidential content stays in employer systems, and every record the user keeps is written at meaning grain — employer-safe by construction.

## Hard content rules

1. **Employer-readable assumption:** anything committed may be read by the employer once the repo sits on a corp device. Write accordingly.
2. **One-way flow, generic in, nothing employer-derived out:** committed content is employer-generic convention only. Anything derived from employer docs, systems, code, or confidential context is NEVER committed or pushed here — it stays machine-local on the work device (`local/`, gitignored). This mirrors the standing IP rule in both directions: nothing from work leaves the employer; nothing of the user's private content enters this repo.
3. **No secrets of any kind** — no values, no secret-manager item names, no tokens, no placeholders that reveal private infrastructure.
4. **Not a bridge:** this repo is not a sync channel; work state never leaves the work device through it.
5. **Open-tool voice and content scope (design principle 18):** committed content speaks as an open, user-generic work tool — "the user" (or "the maintainer"/"the author" in provenance contexts), never a named owner or a personal-ecosystem counterpart — and describes only the tool ITSELF: knowledge about how any particular user relates the tool to the rest of their estate (what they keep out of it, inventories of what stays elsewhere) is that user's own knowledge and never enters the seed.

## Layout

- `CLAUDE.md` — this file: identity + hard rules, loaded by upstream build sessions and by work-side sessions if the sanctioned tooling reads it.
- `UNFOLD.md` — the installer: detect (work docs + device) → resolve the adaptation ledger → generate the adapted form into `local/`. Tooling-agnostic plain markdown — followable by any sanctioned agent, or manually.
- `corpus/` — the genome: the generic convention modules and portable skills the unfold selects from.
- `skeleton/` — the phenotype (principle 30): the installed estate's concrete directory tree, shipped as ready template files (state files, registry + job-registry schemas, per-project home template); the unfold copies it, then adapts — structure is never re-derived. `skeleton/README.md` draws the tree once.
- `CHANGELOG.md` — the update manifest: one entry per seed version (SemVer git tags), naming the changed modules and the derived layers they affect; read by `UNFOLD.md` §Update against the installed version.
- `text_docs/design.md` — design record: the installation-package model, settled principles, the adaptation-points ledger. `text_docs/` also holds idea/direction notes.
- `knowledge/` — reference research digests (committed; same employer-readable discipline).
- `local/` — gitignored; holds the unfold's ledger + log, and the degraded-fallback state form. The unfold's real output is the founded ESTATE at the root A4 chooses (outside this clone). Nothing work-machine-specific is ever committed.
- `TODO.md` — gitignored, per the task convention (`corpus/task-convention.md`); tracked in the maintainer's task system off this machine. On the work machine, the estate hub's task head takes this role — the clone itself never carries work state post-install.

