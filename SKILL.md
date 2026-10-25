---
name: pharma-stats
description: Biostatistics workflow for clinical trials in pharma (SDTM → ADaM → TLF) with Claude Code, in SAS or R. Use when writing, reviewing, or QCing statistical programs, when starting a new study, or when the user wants a human-in-the-loop workflow: the statistician makes the decisions and runs the code, Claude Code writes small, self-contained snippets. Sets up a layered CLAUDE.md project template, exploration snippets, a decision log, QC commands, and reviewer subagents.
---

# Pharma Stats — Human-in-the-Loop Biostatistics with Claude Code

Clinical trial programming fails with AI for one specific reason: a derivation
is a chain of small hidden assumptions, and an agent guesses each one silently.
By the time it finishes, you are debugging ten guesses at once. This skill flips
the order: **decide first, derive second, and make every decision visible in
the data before it becomes code.**

## Install into a project

Copy the `templates/` folder contents into the study project root, then
replace every `[placeholder]` with the real study information:

```
study-project/
├── CLAUDE.md              ← root: map + iron rules (templates/CLAUDE.md)
├── adam/CLAUDE.md         ← ADaM conventions
├── tlf/CLAUDE.md          ← TLF conventions
├── sdtm/CLAUDE.md         ← SDTM read-only conventions
├── specs/CLAUDE.md        ← spec read-only declaration
├── docs/STUDY_MAP.md      ← project index (maintain by hand)
├── docs/DECISIONS.md      ← decision log (see below)
└── .claude/
    ├── commands/          ← /check-log /qc-tlf /new-adam
    ├── agents/            ← study-explorer / tlf-reviewer
    └── settings.json      ← permissions + hooks
```

Claude Code loads the root CLAUDE.md every session, plus the CLAUDE.md of
whichever directory is being worked in. Context stays small because each file
only covers its own directory.

## The hybrid loop

Never ask for a whole derivation. Work in small, verifiable rounds:

1. **One question, one snippet.** Ask for an exploration snippet, not a
   derivation. Example: "What distinct DSDECOD values exist in DS?"
2. **The user runs it.** The snippet must be self-contained: it loads its own
   libraries and data at the top, so it runs in a fresh R session. The user
   runs it (RStudio, Source or run selection) and sees the output.
3. **The user decides.** The user pastes the output back and makes the call,
   e.g. "screen failures stay out, these three decodes map to completed."
4. **Record the decision.** Write it to `docs/DECISIONS.md` with the evidence
   (the R output), the decision, and the date.
5. **Then derive.** Only now is the derivation written, with a comment pointing
   back to the decision ID (e.g. `# D-004: screen failures excluded`).

Batch the exploration, not the derivation: for one dataset, ask for 3–5
snippets at once (distinct values, missingness, date ranges, duplicates,
cross-checks against DM), run them all, and make several decisions in one round.

## Non-negotiable rules

These are baked into `templates/CLAUDE.md` and `templates/.claude/settings.json`.
Enforce them on every task:

- **Re-read before editing.** Before any Edit or Write, Read the file's
  current contents first, even if it was already read in this session. The
  user edits by hand in RStudio; a remembered version may be stale, and editing
  from memory overwrites their work. A PreToolUse hook on Edit/Write injects
  this reminder before every edit.
- **The user runs the code by default.** Do not execute R/SAS code unless the
  user explicitly says "you run it." Write the code, say which file to run and
  how, and wait for the output. Running Rscript/SAS is set to "ask" in
  settings.json, so execution always needs approval.
- **Snippets must be self-contained.** No reliance on intermediate variables
  from the agent's session. If a chunk depends on earlier steps, state the
  setup steps first.
- **One task per session.** One dataset or one table per session; switch
  tasks by starting a new session. On `/compact`, keep the key decisions.
- **Specs are read-only and are the only truth source.** Never modify
  `specs/` without explicit approval. If a spec looks wrong, stop and report it.
- **Metadata only, never patient data.** define.xml, specs, and data
  dictionaries are fine in conversation. Raw subject-level data is not.
- **Logs must be clean.** Zero ERROR; every WARNING explained.
- **Humans review.** All code changes need human review before formal analysis
  (GxP). A big change starts in Plan mode with the plan saved for review.

## Commands and agents (from templates/.claude/)

- `/check-log <log>` — scan a SAS/R log for ERROR and WARNING, grouped with
  line numbers, and give a pass/fail verdict.
- `/qc-tlf <program>` — QC a TLF program against its shell: titles, footnotes,
  populations, N counts, decimals, units, clean log, no hardcoded values.
- `/new-adam <dataset>` — scaffold a new ADaM program from the spec, with an
  input-check section and a "to confirm" list for anything the spec leaves
  unclear. Never invent derivation logic.
- `study-explorer` (agent) — maps a new study: scans the directories and
  builds/updates `docs/STUDY_MAP.md`. Marks unknowns `[to fill]`, never guesses.
- `tlf-reviewer` (agent) — independent QC, second-person style: verifies
  outputs against shell and SAP, independently recomputes at least two numbers
  from ADaM, and writes a report to `docs/review_YYYYMMDD_<id>.md`. It reports
  problems; it does not fix them.

## Decision log

`docs/DECISIONS.md` is the audit trail and the memory that survives
`/compact`. Format: one row per decision — ID, date, question, evidence (the R
output), decision, downstream impact. When a derivation rule is written, cite
its decision ID in a code comment. When a spec version changes, note which
decisions it affects.

## Compliance notes

- Use a company-IT-approved deployment (e.g. Claude via Bedrock or an
  enterprise plan). Do not send data to a public API.
- Keep session logs for audit traceability.
- This skill is an efficiency tool. It does not change the SOP requirements
  for independent QC and dual review.
