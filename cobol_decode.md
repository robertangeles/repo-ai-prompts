# COBOL Decode Protocol — Terrain-First Multi‑Pass (Copilot, Selection‑Scoped)

## Operator Quickstart
1. Open the COBOL file in VS Code.
2. **Pass 0 only:** select the full file (Ctrl+A). Run Pass 0 to generate the Terrain Map.
3. For later passes, select the exact line ranges reported by the Terrain Map.
4. Paste **SESSION** and **RULES** at the start of every Copilot request.
5. Run one pass at a time. Do not mix passes.
6. Keep outputs under version control. Save to `/docs/{{PROGRAM-ID}}/{{PASS_NAME}}.md`.

---

## SESSION
```
SESSION
- Program: {{PROGRAM-ID}}
- File path: {{PATH}}
- Lines in scope: {{START_LINE}}-{{END_LINE}}
- Pass: {{PASS_NAME}}  (Terrain | Inputs | Processing | Outputs | Prototype SQL | Mapping | Gaps | Lineage)
- Continuation: {{NEW | CONTINUE:KEY123}}
```
Purpose: scope anchor for humans and audit. Copilot still uses the active selection.

---

## RULES
```
- Use only the selected lines in scope. Ignore everything else.
- Build an Evidence Ledger first. Quote every claim with exact line numbers and snippets.
- If evidence is missing, write [Unverified] and "I do not have access to that information."
- Style: short sentences. Active voice. No em dashes. No speculation.
- Output cap: 120 lines, then stop.
- End with: NEXT PROMPT KEY: {{KEY}}
```
Keep these rules in every pass.

---

## Evidence Ledger Template
```
||ID||Type||Line range||Exact snippet||Why||
|EV1||||||
|EV2||||||
```
Use this first in every pass.

---

# Pass 0 — Terrain Map  *(run this first)*
**Selection:** the entire file.  
**Goal:** produce a complete map so you never read COBOL manually.

**TASKS**
1. **Section Map**
   - Show start and end line numbers for: IDENTIFICATION DIVISION, ENVIRONMENT DIVISION, DATA DIVISION, PROCEDURE DIVISION.
2. **Paragraph Index**
   - List every paragraph label with its start line.
   - List any `PERFORM` or `PERFORM THRU` targets.
3. **SQL Index**
   - List all `EXEC SQL` blocks with line ranges.
   - Show type: SELECT, INSERT, UPDATE, DELETE, MERGE.
   - Extract target table names if visible.
4. **File Index (FD)**
   - List each `FD` record with start line.
   - If record 01 layout appears, show its 01 name and line range.
5. **Copybooks and Includes**
   - List each `COPY` and the line where it appears.
6. **Driver Hints**
   - Identify likely driver paragraphs or main loops by frequency of being called or the presence of READ loops.

**OUTPUT FORMAT**
```
### SECTION MAP
||Section||Start Line||End Line||
|IDENTIFICATION DIVISION|1|12|
|ENVIRONMENT DIVISION|13|65|
|DATA DIVISION|66|580|
|PROCEDURE DIVISION|581|8120|

### PARAGRAPH INDEX
||Paragraph||Start Line||PERFORM Targets||
|1000-INIT|600|N/A|
|2000-MAIN|620|3000-READ THRU 3999-EXIT|

### SQL INDEX
||Line Range||Type||Target||EV||
|1220–1248|SELECT|CLAIMS_RAW|EV17|
|4120–4170|INSERT|CLAIMS_STATUS|EV44|

### FILE INDEX
||FD Name||Start Line||Record 01 Name||01 Lines||EV||
|IN-CLAIMS|75|IN-CLAIMS-REC|80–140|EV5|
|OUT-REJECT|220|REJECT-REC|221–260|EV9|

### COPYBOOKS
||Copy Name||Line||EV||
|CLMREC.CPY|78|EV6|

### DRIVER HINTS
- Main driver: 2000-MAIN at line 620.
- Primary loop: 3000-READ reads IN-CLAIMS and calls 4000-PROCESS.
```
End with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 1 — Inputs  (Section 2)
**Selection:** use the Terrain Map line numbers. Select FILE SECTION, the 01 records, related COPY blocks, and all `EXEC SQL SELECT` ranges.

**TASK**
- List all flat files and SQL cursors.
- For each: COBOL names, inferred meaning, likely data type, record layout guess. Mark unknowns `[Unverified]`.

**Tables**
```
Sources
||Source ID||Type||Name||Where (EV)||Purpose||

File Layouts
||Source ID||Level/Name||PIC/USAGE||Occurs||Inferred SQL type||EV||

SQL Inputs
||Cursor/Stmt||Line range||SQL target||Key columns||EV||
```

---

# Pass 2 — Processing  (Section 3)
**Selection:** the main loop and processing paragraphs found in Terrain Map.

**TASK**
- Stepwise logic. One step per bullet. Tie each step to Evidence IDs.
- For each step: paragraph, scope (always | conditional | loop), controlling flag, per-record or batch, transforms, flags or codes, constants, dependencies, error handling.

**Format**
```
Step N: Paragraph=XXXX. Scope=conditional (flag=ELIGIBLE). Per-record.
Uses EV3, EV7. Transform: amount = raw / 100. On error: write reject EV12.
```

---

# Pass 3 — Outputs  (Section 4)
**Selection:** all `EXEC SQL` write operations and WRITE statements. Include commit or checkpoint logic.

**TASK**
- For each output: show SQL or WRITE target, effect, per-record vs batch, commit behavior.
- Provide a field mapping table.

**Tables**
```
Outputs
||Op||Target||EV||Per-record or batch||Commit behavior||

Field Mapping
||Source Field||Transform lineage||Target Column||EV||
```

---

# Pass 4 — Prototype SQL  (Section 5)
**Selection:** only logic evidenced in prior passes.

**TASK**
- SQL that mirrors evidenced logic only.
- Label gaps `[Unverified]`.
- Add Databricks notes if relevant.

**Sections**
1. CTEs for inputs  
2. Transform blocks tied to EV IDs  
3. Final INSERT or UPDATE statements  

---

# Pass 5 — Field Mapping Summary  (Section 6)
**Selection:** code that computes or moves fields that end up in outputs.

**TASK**
- Consolidated mapping table across all targets.

**Table**
```
||COBOL Var||Meaning||Type||Routine||Transform lineage||Mapped To (Table.Column)||EV||
```

---

# Pass 6 — Gaps + Bias Check  (Section 7 and 7.1)
**Selection:** external module calls, unresolved copybooks, ALTER, ON EXCEPTION, SQLCODE handling, FILE STATUS checks.

**TASK**
- List gaps with tags: MISSING MODULE, UNAVAILABLE COPYBOOK, UNKNOWN RULE, UNOBSERVED PATH.
- State impact and a proposed test.
- Complete Bias Checklist in short answers.

**Tables**
```
Gaps
||Tag||Where (EV)||Impact||Proposed test||

Bias Checklist
Q1..Qn with short answers. Cite EV where possible.
```

---

# Pass 7 — Data Lineage Summary  (Section 8)
**Selection:** none. Use outputs from prior passes only.

**TASK**
- Build a single lineage table from sources to targets.

**Table**
```
||Source||Source Attrs||Transformation||Target||Target Attr||Join Condition||Rel Type||EVs||
```

---

## Continuations and Output Control
- End every pass with: `NEXT PROMPT KEY: {{KEY}}`
- If output reaches the cap, stop. Use `Continuation=CONTINUE:{{KEY}}` next run.
- On continuation, restate **SESSION**, **RULES**, and the last two lines of the Evidence Ledger.

## Quality Bar
- Scope obedience. Only lines in scope used.
- Evidence density. Each claim has an EV.
- Determinism. No guessing.
- Merge-ready. Tables and Mermaid compile.
- Token control. 120 lines or less. Continuation key present.
- If any item is `[Unverified]`, prepend: `[Unverified] applies to whole output.`
