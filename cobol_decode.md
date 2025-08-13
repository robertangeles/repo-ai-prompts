# COBOL Decode Protocol — Terrain-First Multi-Pass (Copilot, Selection-Scoped, **Markdown Table Output**)

## Operator Quickstart
1. Open the COBOL file in VS Code.
2. **Pass 0 only:** select the full file (Ctrl+A). Run Pass 0 to generate the Terrain Map.
3. For later passes, select the exact line ranges reported by the Terrain Map.
4. Paste **SESSION** and **RULES** at the start of every Copilot request.
5. Run one pass at a time. Do not mix passes.
6. Save outputs to `/docs/{{PROGRAM-ID}}/{{PASS_NAME}}.md`.

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
**Output requirement:** Use **Markdown tables** (pipes and dashes). No HTML. No Confluence wiki syntax. No code fences.

| ID  | Type | Line range | Exact snippet | Why |
|-----|------|------------|---------------|-----|
| EV1 |      |            |               |     |
| EV2 |      |            |               |     |

---

# Pass 0 — Terrain Map  *(run this first)*
**Selection:** the entire file.  
**Goal:** produce a complete map so you never read COBOL manually.

**TASKS (each as a separate table in this order)**
1. Section Map — start and end lines for all divisions.  
2. Paragraph Index — all paragraphs with PERFORM targets.  
3. SQL Index — all EXEC SQL with type and target.  
4. File Index — all FD records and 01 record ranges.  
5. Copybooks and Includes.  
6. Driver Hints — brief bullets after the tables.

**TABLE OUTPUT RULES**  
- Use **Markdown tables** only. No HTML `<br/>`. No Confluence wiki syntax. No code fences.  
- One blank line between tables.  
- Keep each table under 40 rows per page. If longer, continue in a second table with a note: “continued”.

### SECTION MAP
**Columns:** Section | Start Line | End Line | EV

| Section               | Start Line | End Line | EV  |
|-----------------------|------------|----------|-----|
| IDENTIFICATION DIVISION |            |          | EV  |
| ENVIRONMENT DIVISION    |            |          | EV  |
| DATA DIVISION           |            |          | EV  |
| PROCEDURE DIVISION      |            |          | EV  |

### PARAGRAPH INDEX
**Columns:** Paragraph | Start Line | PERFORM Targets | EV

| Paragraph   | Start Line | PERFORM Targets                 | EV  |
|-------------|------------|----------------------------------|-----|
| 1000-INIT   |            |                                  | EV  |
| 2000-MAIN   |            | 3000-READ THRU 3999-EXIT         | EV  |

### SQL INDEX
**Columns:** Line Range | Type | Target | EV

| Line Range | Type    | Target          | EV  |
|------------|---------|-----------------|-----|
|            | SELECT  |                 | EV  |
|            | INSERT  |                 | EV  |

### FILE INDEX
**Columns:** FD Name | Start Line | Record 01 Name | 01 Lines | EV

| FD Name    | Start Line | Record 01 Name | 01 Lines | EV  |
|------------|------------|----------------|----------|-----|
| IN-CLAIMS  |            | IN-CLAIMS-REC  |          | EV  |
| OUT-REJECT |            | REJECT-REC     |          | EV  |

### COPYBOOKS AND INCLUDES
**Columns:** Copy Name | Line | EV

| Copy Name   | Line | EV  |
|-------------|------|-----|
| CLMREC.CPY  |      | EV  |
| ERRHAND.CPY |      | EV  |

### DRIVER HINTS
- Main driver paragraph(s): `<name>` at line `<n>`.
- Primary loop(s): list paragraph names and relationships, for example: `3000-READ` reads `IN-CLAIMS` and calls `4000-PROCESS`.

End Pass 0 with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 1 — Inputs  (Section 2)
**Selection:** use Terrain Map line numbers for FILE SECTION, 01 records, related COPY blocks, and all `EXEC SQL SELECT` ranges.

**Output requirement:** Use **Markdown tables** only. No HTML. No Confluence wiki syntax. No code fences.

### Sources
| Source ID | Type | Name | Where (EV) | Purpose |
|-----------|------|------|------------|---------|

### File Layouts
| Source ID | Level/Name | PIC/USAGE | Occurs | Inferred SQL type | EV |
|-----------|------------|-----------|--------|--------------------|----|

### SQL Inputs
| Cursor/Stmt | Line range | SQL target | Key columns | EV |
|-------------|------------|------------|-------------|----|

---

# Pass 2 — Processing  (Section 3)
**Selection:** the main loop and processing paragraphs found in Terrain Map.

**Task format:** use a concise bullet list. Tie each step to Evidence IDs. Short sentences.  
**If a table helps, use Markdown tables for repeated patterns.**

**Step pattern example**
- Step N. Paragraph = `XXXX`. Scope = conditional (flag = `ELIGIBLE`). Per-record. Uses EV3, EV7. Transform: `AMOUNT = RAW / 100`. On error: write reject EV12.

**Optional step table**
| Step | Paragraph | Scope      | Flag      | Mode      | Transforms                 | Errors         | EVs      |
|------|-----------|------------|-----------|-----------|----------------------------|----------------|----------|
| 1    | 4000-PROC | conditional | ELIGIBLE  | per-record| AMOUNT = RAW / 100         | write reject   | EV3, EV7 |

End Pass 2 with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 3 — Outputs  (Section 4)
**Selection:** all `EXEC SQL` write operations and WRITE statements. Include commit or checkpoint logic.

**Output requirement:** Markdown tables only.

### Outputs
| Op     | Target         | EV  | Mode        | Commit behavior |
|--------|----------------|-----|-------------|-----------------|

### Field Mapping
| Source Field | Transform lineage | Target Column | EV  |
|--------------|-------------------|---------------|-----|

---

# Pass 4 — Prototype SQL  (Section 5)
**Selection:** only logic evidenced in prior passes.

**Output requirement:** Markdown code blocks for SQL are OK. Tables remain Markdown tables.

### Sections
1. CTEs for inputs  
2. Transform blocks tied to EV IDs  
3. Final INSERT or UPDATE statements

End Pass 4 with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 5 — Field Mapping Summary  (Section 6)
**Selection:** code that computes or moves fields that end up in outputs.

**Output requirement:** Markdown tables only.

| COBOL Var | Meaning | Type | Routine | Transform lineage | Mapped To (Table.Column) | EV |
|-----------|---------|------|---------|-------------------|---------------------------|----|

End Pass 5 with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 6 — Gaps + Bias Check  (Section 7 and 7.1)
**Selection:** external module calls, unresolved copybooks, ALTER, ON EXCEPTION, SQLCODE handling, FILE STATUS checks.

**Output requirement:** Markdown tables only.

### Gaps
| Tag                | Where (EV) | Impact | Proposed test |
|--------------------|------------|--------|---------------|

### Bias Checklist
| Question | Answer | EV (optional) |
|----------|--------|---------------|

End Pass 6 with: `NEXT PROMPT KEY: {{KEY}}`

---

# Pass 7 — Data Lineage Summary  (Section 8)
**Selection:** none. Use outputs from prior passes only.

**Output requirement:** Markdown tables only.

| Source            | Source Attrs          | Transformation        | Target          | Target Attr | Join Condition             | Rel Type | EVs     |
|-------------------|-----------------------|-----------------------|-----------------|-------------|----------------------------|---------|---------|

End Pass 7 with: `NEXT PROMPT KEY: {{KEY}}`

---

## Continuations and Output Control
- End every pass with: `NEXT PROMPT KEY: {{KEY}}`
- If output reaches the cap, stop. Use `Continuation=CONTINUE:{{KEY}}` next run.
- On continuation, restate **SESSION**, **RULES**, and the last two lines of the Evidence Ledger.

## Quality Bar
- Scope obedience. Only lines in scope used.
- Evidence density. Every claim has an EV.
- Determinism. No guessing.
- Merge-ready. Tables render in GitHub and paste cleanly to Confluence.
- Token control. 120 lines or less. Continuation key present.
- If any item is `[Unverified]`, prepend: `[Unverified] applies to whole output.`
