As a COBOL developer from the top 0.1%, you are helping a data engineering team reverse engineer undocumented Pro*COBOL batch programs. These programs read from flat files or source tables and write to relational database tables using embedded SQL. The goal is to rebuild the same logic in a modern data platform. The audience is a modern data engineer who does not know COBOL.
For the COBOL code I provide, return the following structured breakdown in clean Confluence ready format.

SECTION 1: PROGRAM OVERVIEW
- Describe the overall purpose of the COBOL job in one or two sentences. 
- Summarize the data flow, such as "reads claims from a flat file, applies eligibility rules, and updates the CLAIMS_STATUS table."

SECTION 1.1: I/O DIAGRAM

Generate a comprehensive diagram illustrating the Input-Processing-Output (IPO) flow of the COBOL code.
The diagram should clearly represent:
- Inputs: Data sources, formats, and entry points.
- Processing: Key logic, transformations, and decision points within the COBOL code.
- Outputs: Final data structures, destinations, and formats.

The audience includes both product owners and data engineers, so the diagram should balance technical depth with clarity. Use annotations or callouts to explain complex logic where necessary, and ensure the visual layout supports intuitive understanding of how the code operates end-to-end.

SECTION 2: INPUT PHASE

List all input sources, including flat file names and any SQL SELECT statements.
For each input source:
- Show the COBOL variable names
- Suggest what each field probably means
- Guess the likely data type (CHAR, NUMERIC, DATE, etc.)
- If possible, describe the flat file layout or record structure

SECTION 3: PROCESSING PHASE

Describe each major step of the business logic in plain English. Describe the structure and the logic (loops, conditionals, GO TOs, PERFORMs, etc.) and indicate key sections like initialization, main processing loop, and end-of-job logic.

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

SECTION 4: OUTPUT PHASE

List all SQL INSERT, UPDATE, DELETE, or MERGE statements. Identify all outputs, reports, or written files. These outputs might be INSERTS, UPDATES, or a FILE written in a file system.
For each output:
- Show the SQL block of INSERT or UPDATE or both
- Describe what each statement or code block is doing
- Indicate which COBOL fields are being written to which target fields
- Note if output happens per record or in a batch
- Mention any commit strategy (such as COMMIT every 500 rows)

SECTION 5: PROTOTYPE SQL CODE

- Rewrite the core logic that mirrors how it will function using SQL
- Suggest transformation logic if migrating to Databricks

SECTION 6: FIELD MAPPING SUMMARY

Present a table with the following columns:
- COBOL Variable
- Inferred Meaning
- Data Type
- COBOL Routine
- Transformations or Computations (include the full lineage of the value's derivation, such as calculations, conditional logic, business rules, or intermediate assignments)
- Mapped To (in Table.Field format)
- For each field, trace and show how the final value was constructed from its original source — whether from a flat file, SQL SELECT, constant assignment, or derived field. Clearly state whether the value is:
	- Directly copied from input
	- Calculated using arithmetic or business rules
	- Assigned conditionally based on flags, statuses, or codes
	- Modified through multiple intermediate variables before reaching final output

SECTION 7: GAP ANALYSIS

List all unknown, missing, or unclear logic.
For each gap:
- Include the COBOL routine or paragraph name where it occurs
- Describe what is missing or unclear
- Use tags like MISSING MODULE, UNKNOWN RULE, or UNAVAILABLE COPYBOOK
- Add a short guess of what the logic might do if you can infer it

SECTION 7.1: Bias and Fairness Review Checklist
For each AI-generated output, assess:
- Are any fields or logic disproportionately affecting certain groups?
- Are hardcoded rules or flags based on assumptions?
- Is the training data (e.g., legacy COBOL logic) representative of current business rules?

SECTION 8: DATA LINEAGE SUMMARY

Analyze the program’s complete data lineage, from source to target. Focus only on functional COBOL code (exclude comment lines starting with *). Provide a detailed table and narrative that allows modern data engineers to fully trace every field’s journey.

Include a complete lineage summary table with these columns:
- Source: Source file, source table, or external module
- Source Attributes: Fields or variables used from the source
- Transformation: Detail how the data is modified (calculations, conversions, lookups, etc.)
- Target: Destination file or target table
- Target Attribute: Name of the output field or variable
- Join Condition: All conditions that link the source and target (include full SQL conditions)
- Relationship Type: Specify one-to-one, one-to-many, many-to-one, etc.

Additional Requirements:
- Ensure every table touched by the program is represented — including flat files, input tables, working/intermediate tables, cursor result sets, and final output targets.
- Show full lineage paths, from initial source attribute to final target attribute, including all intermediate calculations or transformations.
- Track all cursor-based data flows: what each cursor SELECTs, how it’s looped through, and how results are written.
- Explicitly document conditional data routing — for example, when different rules send data to different output tables.
- Include the data flow into reject/error-handling paths (e.g. RISKEQ_ERROR), including which logic triggers them.
- If external modules are called (e.g. SYAGECAL), flag their data dependencies and outputs even if their internal logic is unknown.
- Highlight composite keys and any conditional joins or lookup enrichment steps (e.g. if ABP_TYPE = 'Y' then join to PHIAC_ABP).
- Provide a supporting narrative alongside the table that explains the overall structure, joins, and flow patterns, especially any complex routing or transformation chains.

MONITOR HALLUCINATION

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

FINAL INSTRUCTION

Return the entire response in Confluence ready format with clear headings. 

What would a top 0.1% expert in this field think?
