# Pharma Stats Skill for Claude Code

A Claude Code skill and project template for biostatisticians doing clinical
trial statistical programming (SDTM → ADaM → TLF) in SAS or R.

## The idea

End-to-end AI derivation fails because a derivation is a chain of small hidden
assumptions, and the agent guesses each one silently. This skill flips the
order: **decide first, derive second.** The statistician makes the decisions
and runs the code; Claude Code writes small, self-contained snippets. Every
decision is visible in the data before it becomes code, and recorded in a
decision log.

## What's inside

- `SKILL.md` — the skill itself: the hybrid loop, the non-negotiable rules,
  and how to use the commands and agents.
- `templates/` — a drop-in project template:
  - Layered `CLAUDE.md` files (root + `adam/` + `tlf/` + `sdtm/` + `specs/`)
  - `docs/STUDY_MAP.md` — project index, maintained by hand
  - `docs/DECISIONS.md` — decision log / audit trail
  - `.claude/commands/` — `/check-log`, `/qc-tlf`, `/new-adam`
  - `.claude/agents/` — `study-explorer`, `tlf-reviewer`
  - `.claude/settings.json` — permissions (Rscript/SAS runs need approval)
    and hooks (a reminder to re-read a file before every edit)

## Use it as a skill

Copy this folder to `~/.claude/skills/pharma-stats/` (all projects) or to a
project's `.claude/skills/pharma-stats/`, then invoke it with
`/pharma-stats` or let Claude Code pick it up when the task matches.

## Use it as a project template

Copy the contents of `templates/` into your study project root and replace
every `[placeholder]` with the real study information. Start with
`study-explorer` to map a new study into `docs/STUDY_MAP.md`.

## Core rules (enforced by the template)

1. Re-read a file before editing it — the user edits by hand in RStudio, and
   a remembered version may be stale.
2. The user runs the code by default; Claude Code runs it only when explicitly
   asked.
3. Every snippet is self-contained: it loads its own libraries and data.
4. Specs are read-only and are the only truth source.
5. Metadata only in conversation — never raw subject-level data.
6. Logs must be clean: zero ERROR, every WARNING explained.
7. Humans review all code before formal analysis (GxP).

## Compliance

Use a company-IT-approved deployment (e.g. Claude via Bedrock or an
enterprise plan). Keep session logs for audit traceability. This skill does
not change SOP requirements for independent QC and dual review.

## License

MIT — free to use and adapt.
