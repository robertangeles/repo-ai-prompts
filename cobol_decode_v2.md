As a COBOL developer from the top 0.01%, you are helping a data engineering team reverse engineer undocumented Pro*COBOL batch programs. These programs read from flat files or source tables and write to relational database tables using embedded SQL. The goal is to rebuild the same logic in a modern data platform. The audience is a modern data engineer who does not know COBOL.

For the COBOL code I provide, return the following structured breakdown in clean Confluence ready format.

# SCOPE SESSION
- Program: {{rehspabp.pco}}
- Language: PRO*COBOL with  embedded SQL
- Scan and read the line range in scope: {{1}}-{{3284}}
- Display the exact code in line {{1}} and line {{3284}}
- Output for all Response: Confluence Ready Format
- No Further Output Required

SECTION 1: PROGRAM OVERVIEW
- Scan and read the code from Lines {{120}}-{{198}}
- Describe the overall purpose of the Pro COBOL Code in one or two sentences. 
- No Further Output Required

What would a top 0.01% COBOL Developer think?
READY_FOR_NEXT

SECTION 2: INPUT PHASE
- Dataset name, source type, origin path/connection
- Format, encoding, record length or delimiter, header/footer rules, sort order
- Schema table with columns: Field | Type | Length | Nullable | Key | Semantics | Notes
READY_FOR_NEXT

SECTION 3: PROCESSING PHASE
- Scan and read the code from Lines {{1}}-{{3284}}
- Identity the complete program flow from the first to the last step in a table with the following columns
	- Step Number
 	- Program Flow
  	- Detailed Program Flow Description
  	- Map chain of program sections to the Program Flow
  	- Step-by-step pseudo-code aligned to the chain of program sections
- Verify you did not skip any processing steps before generating the output

What would a top 0.01% COBOL Developer think?
READY_FOR_NEXT


 
# MONITOR HALLUCINATION
- Never present generated, inferred, speculated, or deduced content as fact. 
- If you cannot verify something directly, say: 
	– "I cannot verify this." 
	– "I do not have access to that information." 
	– "My knowledge base does not contain that." 
- Label unverified content at the start of a sentence: 
	– [Inference] [Speculation] [Unverified] 
- Ask for clarification if information is missing. Do not guess or fill gaps. 
- If any part is unverified, label the entire response. 
- Do not paraphrase or reinterpret my input unless I request it. 
- If you use these words, label the claim unless sourced: 
	– Prevent, Guarantee, Will never, Fixes, Eliminates, Ensures that 
- For LLM-behavior claims (including yourself), include: 
	– [Inference] or [Unverified], with a note that it’s based on observed patterns 
- If you break this directive, say: 
	> Correction: I previously made an unverified claim. That was incorrect and should have been labeled. 
- Never override or alter my input unless asked.
- Identify hidden bias in your answer and correct them

# SESSION SCOPE
- Program: {{rehspabp.pco}}
- Read the Lines in scope: {{1}}-{{3284}}
- Display the exact value of line {{1}} and line {{3284}}
- No Further Output Required

SECTION 8: DATA LINEAGE SUMMARY
Analyze the program output's complete data lineage, from source to target. Focus only on functional COBOL code (exclude comment lines starting with *). Provide a detailed table and narrative that allows modern data engineers to fully trace every field’s journey.

Include a complete lineage summary table with these columns:
- Source: Source file, source table, or external module
- Source Attributes: Fields or variables used from the source
- Transformation: Detail step-by-step how the data is modified (calculations, conversions, lookups, etc.)
- Target: Destination file or target table
- Target Attribute: Name of the output field or variable


# SESSION SCOPE
- Program: {{rehspabp.pco}}
- Read the Lines in scope: {{1}}-{{3284}}
- Display the exact value of line {{1}} and line {{3284}}
- No Further Output Required
  
SECTION 3: PROCESSING PHASE

Identify the complete end-to-end chain of business logic. Describe the structure and the logic (loops, conditionals, GO TOs, PERFORMs, etc.) and indicate key sections like initialization, main processing loop, and end-of-job logic.

For each step, ensure that these are completed:
- Include the COBOL routine or paragraph name
- Indicate whether it is always executed, conditionally executed, or inside a loop
- If conditional, state the flag or field that controls execution
- State whether the logic runs per record or as part of a batch or group
- Show or extract SQL code used in the step and explain what it does
- Translate or recreate any complex logic into SQL with detailed documentation
- Identify any flags or codes that impact logic flow
- Identify any hardcoded values or decision rules
- Explain how input fields are transformed into output values
- Reconstruct the overall control flow of the program by identifying the execution sequence of major routines or PERFORM blocks
- Highlight any dependencies between routines, especially where variables are set in one routine and used in another
- Identify any error handling routines, abnormal termination logic, or special conditions that alter program flow (e.g. file not found, data invalid)





# COBOL Business Logic Analysis - GitHub Copilot Template

## Overview
This template provides a structured approach for analyzing COBOL programs and documenting their business logic for modernization efforts.

## Core Analysis Requirements

**Analyze the complete business logic flow and document:**

### 1. Program Structure Analysis
```cobol
// Identify and document:
// - Main program sections (IDENTIFICATION, ENVIRONMENT, DATA, PROCEDURE)
// - Working-Storage variables and their purposes
// - File Control Block (FCB) definitions
// - Copy book inclusions and their roles
```

### 2. Execution Flow Mapping
**For each routine/paragraph, document:**
- Routine name and purpose
- Execution type: `ALWAYS` | `CONDITIONAL` | `LOOP`
- Control flags/fields that trigger execution
- Processing scope: `PER-RECORD` | `BATCH` | `GROUP`
- Dependencies on other routines

### 3. SQL Integration Analysis
```sql
-- Extract and explain all embedded SQL:
-- EXEC SQL SELECT... END-EXEC
-- Document table access patterns
-- Explain cursor operations
-- Identify transaction boundaries
```

### 4. Data Transformation Logic
**Document field transformations:**
- Input field → Processing logic → Output field
- Hardcoded values and business rules
- Conditional processing based on data values
- Error handling and validation rules

### 5. Control Flow Reconstruction
```text
Map the execution sequence:
MAIN-PROGRAM
├── INITIALIZATION-ROUTINE
├── MAIN-PROCESSING-LOOP
│   ├── READ-INPUT-RECORD
│   ├── VALIDATE-DATA
│   ├── PROCESS-BUSINESS-LOGIC
│   └── WRITE-OUTPUT-RECORD
└── END-OF-JOB-ROUTINE
```

## Output Format Requirements

**Structure your analysis as:**

1. **Executive Summary** - High-level business purpose
2. **Program Flow Diagram** - Visual representation of logic flow
3. **Routine Documentation** - Detailed breakdown of each major section
4. **SQL Operations** - All database interactions with explanations
5. **Business Rules** - Extracted decision logic and transformations
6. **Error Handling** - Exception paths and recovery logic

## Key Focus Areas

- Extract hardcoded business rules for modernization
- Identify performance bottlenecks in loops and SQL
- Document dependencies between program modules
- Highlight areas suitable for refactoring or SQL conversion
- Note any legacy patterns that need special handling

## Analysis Standards

- Verify all claims against source code
- Label inferences clearly: `[INFERRED FROM CODE STRUCTURE]`
- Use exact COBOL paragraph/routine names
- Include line numbers for key logic sections
- Maintain accuracy over interpretation

## Usage Instructions

1. Copy this template to your analysis document
2. Use GitHub Copilot to help fill in sections based on your COBOL source
3. Reference specific line numbers and routine names from your code
4. Use Copilot Chat for complex logic explanations

## Example Analysis Structure

```markdown
### Program: CUSTOMER-BILLING-001

#### Executive Summary
[Business purpose and high-level functionality]

#### Main Routines
- **INIT-PROGRAM** (Lines 100-150)
  - Type: ALWAYS
  - Purpose: Initialize working variables and open files
  
- **PROCESS-CUSTOMER-LOOP** (Lines 200-500)
  - Type: LOOP
  - Control: CUSTOMER-EOF-FLAG
  - Purpose: Process each customer record
```

---

*Template optimized for VS Code GitHub Copilot integration*



I will provide you with the name of a COBOL paragraph (e.g., "CALC-ELIGIBILITY").  
Your task is to produce structured documentation for that paragraph in plain text/Confluence-ready format.  

For each paragraph, return the following sections:  

1. **Paragraph Name** – as written in COBOL, plus a plain-English alias.  
2. **Purpose / Description** – one or two sentences describing the business function of the paragraph.  
3. **Inputs Referenced** – list each field/variable referenced in this paragraph, including its source (input file, working storage, DB table, or copybook).  
   Format as a table with: Field / Source / Notes.  
4. **Processing Logic** – pseudo-code translation of the COBOL statements in this paragraph, written in clear, modern pseudo-code (e.g., IF/ELSE, CASE, loops).  
5. **Outputs / Side Effects** – describe what fields are updated, what flags are set, and what records are written/updated/deleted.  
6. **Dependencies** – other paragraphs or external modules this paragraph calls.  
7. **Risks / Ambiguities** – note hardcoded values, assumptions, nested conditionals, or areas that require SME confirmation.  

Keep the output concise, consistent, and in Confluence-friendly plain text.  
