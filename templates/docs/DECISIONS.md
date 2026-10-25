# Decision Log

> One row per decision. This is the audit trail and the memory that survives
> `/compact`. When a derivation rule is written, cite its decision ID in a code
> comment (e.g. `# D-004: screen failures excluded per DS check`).
> When a spec version changes, note which decisions it affects.

| ID | Date | Question | Evidence (R output) | Decision | Downstream impact |
|----|------|----------|---------------------|----------|-------------------|
| D-001 | YYYY-MM-DD | [e.g. Which DSDECOD values count as completed?] | [e.g. table(ds$DSDECOD): COMPLETED=120, ...] | [e.g. COMPLETED + EARLY TERM map to completed; screen failures excluded] | [e.g. ADSL DISPFL derivation, T1.1 disposition table] |
