# Pro*COBOL Reverse Engineering — Step by Step (Copilot, Markdown Tables)

Audience: engineers who do not read COBOL daily.  
Goal: extract Inputs, Processing, Outputs, and a verified Data Lineage matrix from **Oracle Pro*COBOL** code without guessing.

---

## How to use
1. Open the Pro*COBOL file in VS Code.
2. For each pass, **select only the lines you want analyzed**.
3. Copy the pass prompt block below into Copilot Chat.
4. Paste at the top: `START_LINE=<first file line of your selection>` and `END_LINE=<last file line>`.
5. Run the pass. Keep outputs under version control.
6. Repeat per pass. You will build the doc set without guesswork.

Keep selections tight. 200–600 lines per run works well.

---

## Zero Guess Rules
- Use only the selected lines.
- Every claim cites at least one Evidence ID (EV).
- If a fact is not in the selection, write `[Unverified]` and “I do not have access to that information.”
- If any row has `[Unverified]`, prepend the first line of the whole output with `[Unverified]`.
- Output **Markdown tables** only. No HTML. No code fences around tables in the output.

---

## Shared Evidence Ledger (put first in every pass output)
Use this table first. Then build the rest from it.

| EV | Kind | SelLn (FileLn) | Line range | Exact snippet | Why |
|----|------|-----------------|------------|---------------|-----|

**Kinds:** DIVISION, PARAGRAPH, PERFORM, FD, REC01, EXEC SQL SELECT, EXEC SQL INSERT, EXEC SQL UPDATE, EXEC SQL DELETE, EXEC SQL MERGE, CURSOR DECLARE, CURSOR OPEN, CURSOR FETCH, CURSOR CLOSE, DYNAMIC SQL PREPARE, DYNAMIC SQL EXECUTE, WHENEVER, COMMIT, ROLLBACK, SAVEPOINT, WRITE, COPY, INCLUDE, SQLCA, ORACA.

**Line numbers:** SelLn starts at 1 inside your selection. Compute FileLn as `START_LINE + SelLn − 1` if START_LINE is known.

---

## PASS 0 — Terrain Map
**Selection:** the full file for this first run.

Paste into Copilot Chat:

```
ROLE
You document Oracle Pro*COBOL. Facts only. No guesses.

SCOPE
- Use only the selected lines.
- Build an Evidence Ledger first, then five indexes.
- Use Markdown tables only. No HTML. No code fences around tables.

TASKS
1) Evidence Ledger (EV1..EVn in scan order). Short snippets.
2) Section Map.
3) Paragraph Index with PERFORM targets.
4) SQL Index.
5) File Index.
6) Copybooks and Includes.

OUTPUT
A) Evidence Ledger table.
B) Section Map
| Section | Start Line | End Line | EV |
|---------|------------|----------|----|

C) Paragraph Index
| Paragraph | Start Line | PERFORM Targets | EV |
|-----------|------------|-----------------|----|

D) SQL Index  (include DECLARE, SELECT, INSERT, UPDATE, DELETE, MERGE)
| Line range | Type | Target | EV |
|------------|------|--------|----|

E) File Index
| FD Name | Start Line | Record 01 Name | 01 Lines | EV |
|---------|------------|----------------|----------|----|

F) Copybooks and Includes  (strict match only)
- Match only lines that begin with `COPY ` or `EXEC SQL INCLUDE ` after trimming spaces.
- Skip lines that start with `*` or `*>`.
- Skip if a quote appears before the token on the same line.
- Print a Find Log first, then the table.

Find Log format:
SelLn=<n> | FileLn=<...> | <literal line>

Table:
| SelLn | FileLn | Form | Name | EV |
|-------|--------|------|------|----|

Finish with a one-line coverage check:
COPY matches: <n>, Table rows: <n>. If counts differ, write `[Unverified] Coverage mismatch` and stop.
```
End Pass 0 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 1 — Inputs
**Selection:** use the line ranges from the Terrain Map for FILE SECTION, 01 records, COPY blocks, and all `EXEC SQL SELECT` ranges.

Paste into Copilot Chat:

```
ROLE
You extract input sources from Oracle Pro*COBOL. Facts only.

SCOPE
- Use only the selected lines.
- Build the Evidence Ledger table first.
- Use Markdown tables only. No HTML. No code fences around tables.

TASKS
1) Evidence Ledger for FD, REC01, EXEC SQL SELECT, CURSOR DECLARE/OPEN, SQLCA/ORACA.
2) File Inputs table.
3) SQL Inputs table.
4) Host Variable Map.
5) Copybooks used inside selection.

OUTPUT
A) Evidence Ledger table.

B) File Inputs
| Source ID | FD Name | Record 01 Name | 01 Lines | EVs |
|-----------|---------|----------------|----------|-----|

C) SQL Inputs
| Cursor/Stmt | Line range | Target | Key columns | EVs |
|-------------|------------|--------|-------------|-----|

D) Host Variable Map
| Host Var | COBOL Var | Level | PIC/USAGE | OCCURS | Indicator Var | EVs |
|----------|-----------|-------|-----------|--------|---------------|-----|

E) Copybooks and Includes
| SelLn | FileLn | Form | Name | EV |
|-------|--------|------|------|----|
```
End Pass 1 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 2 — Processing
**Selection:** main loop paragraphs and any logic blocks from the Terrain Map.

Paste into Copilot Chat:

```
ROLE
You summarize processing logic. Facts only. Short sentences.

SCOPE
- Use only the selected lines.
- Build the Evidence Ledger first.
- Track WHENEVER policies and cursor lifecycle if present.
- Use Markdown tables. No HTML. No code fences around tables.

OUTPUT
A) Evidence Ledger table.

B) Control Policies in Effect
| Paragraph | WHENEVER in effect | Action | Lines | EVs |
|-----------|--------------------|--------|-------|-----|

C) Cursor Lifecycle
| Cursor | DECLARE EV | OPEN EV | FETCH EVs | CLOSE EV | Notes |
|--------|------------|---------|-----------|----------|-------|

D) Stepwise Logic  (one row per step)
| Step | Paragraph | Scope | Flag/Condition | Mode | Transform(s) seen | Errors/Rejects | EVs |
|------|-----------|-------|----------------|------|-------------------|----------------|-----|
```
End Pass 2 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 3 — Outputs
**Selection:** ranges with DML and WRITE, plus commit or checkpoint logic.

Paste into Copilot Chat:

```
ROLE
You extract output effects. Facts only.

SCOPE
- Use only the selected lines.
- Build the Evidence Ledger first.
- Use Markdown tables. No HTML. No code fences around tables.

OUTPUT
A) Evidence Ledger table.

B) SQL DML
| Op (I/U/D/M) | Table | Column hints | Mode (per-record/batch) | Commit behavior | EVs |
|--------------|-------|--------------|--------------------------|-----------------|-----|

C) Positioned Ops (WHERE CURRENT OF)
| Op | Table | Cursor | Line(s) | EVs |
|----|-------|--------|---------|-----|

D) File Writes
| Target file | Record | Condition | EVs |
|-------------|--------|-----------|-----|

E) Transaction Control
| Control | Line(s) | Applies to | EVs |
|---------|---------|------------|-----|
```
End Pass 3 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 4 — Data Lineage
**Selection:** the lines that compute or move fields into outputs, plus relevant SELECT inputs.

Paste into Copilot Chat:

```
ROLE
You produce a verified data lineage matrix from the selection.

SCOPE
- Use only the selected lines and prior EVs.
- Build the Evidence Ledger first.
- No inferred columns or transforms.
- Use Markdown tables. No HTML. No code fences around tables.

OUTPUT
A) Evidence Ledger table.

B) Data Lineage Matrix
| Target (Table.Column) | Source (file field or host var) | Transformation (verbatim) | Join/Keys | EVs |
|-----------------------|----------------------------------|---------------------------|-----------|-----|

If a target column has no evidenced source in the selection, skip the row. Do not guess.
```
End Pass 4 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 5 — Gaps
**Selection:** any place with missing modules, missing copybooks, unknown rules, or unobserved paths.

Paste into Copilot Chat:

```
ROLE
You list only proven gaps. No guesses.

SCOPE
- Use only the selected lines.
- Build the Evidence Ledger first.
- Use Markdown tables. No HTML. No code fences around tables.

OUTPUT
A) Evidence Ledger table.

B) Gaps
| Tag | Where | Impact | Proposed probe/test | EVs |
|-----|-------|--------|---------------------|-----|
Tags: MISSING MODULE, UNAVAILABLE COPYBOOK, UNKNOWN RULE, UNOBSERVED PATH.
```
End Pass 5 with: `NEXT PROMPT KEY: {{KEY}}`

---

## PASS 6 — Summary for Confluence
**Selection:** none. Pull from prior pass outputs only.

Paste into Copilot Chat:

```
ROLE
You prepare a merge-ready summary for Confluence from prior pass outputs. No new facts.

SCOPE
- Do not read new code. Use prior tables only.
- Use Markdown tables. No HTML. No code fences around tables.

OUTPUT
1) Program Overview (two lines max, cite EVs).
2) Inputs (file + SQL tables). Copy from Pass 1.
3) Processing (policies, cursor life, stepwise logic). Copy from Pass 2.
4) Outputs (DML, positioned ops, file writes, transaction control). Copy from Pass 3.
5) Data Lineage Matrix. Copy from Pass 4.
6) Gaps. Copy from Pass 5.
7) Coverage summary: Evidence items used, sections with [Unverified].
```
End Pass 6 with: `NEXT PROMPT KEY: {{KEY}}`

---

## Tips
- If Copilot drifts, reselect a smaller range and rerun.
- Keep the Evidence Ledger dense. Each claim needs an EV.
- Save each pass to its own file: `/docs/<program>/<pass>.md`.
