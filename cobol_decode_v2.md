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
- Lines in scope: {{1}}-{{3284}}
- Pass: {{Terrain}}  (Terrain | Inputs | Processing | Outputs | Prototype SQL | Mapping | Gaps | Lineage)
- Continuation: {{NEW}}
- Display the exact code in line {{1}} and line {{3284}}
- No Further Output Required


I/O DIAGRAM Generate a comprehensive drawio diagram (xml file) illustrating the workflow (Input-Processing-Decision Point-Outcome of Decision Point-Output) of the COBOL code.

General rules to follow:

· Try to avoid overlapping lines in the diagram. Make it user friendly.

· Using different colors to differentiate each item and category. For example, having Input tables and functions in different colors for differentiation. And add a legend for the colors.

· Include a header for each section: inputs, processing, decision points, outcome of decision points, and outputs

· Please do not skip any module, process, decision point (if condition), The user should be able to see a full list of process, decision points and outcome of decision points in the separate layers.

· Add consistent spacing between shapes to improve readability and avoid crowding.

· No \n line breaks (uses &lt;br&gt; for multi-line).

· No & character (uses "and" instead).

The diagram should clearly represent:

Inputs: List down the data sources and external functions.

Processing: List down all the module names within the COBOL code. Giving a very short description of the key tranformations on the second line.

Decision point: List down all the decision points if the processing logic contains more than one outcomes

Output of the decision: List down the result from the decision point (e.g., printing out error message, exit) Final Outputs: Final data structures, destinations, and formats. Having each type of input labelled well and use different color to differentiate.

The audience includes both product owners and data engineers, so the diagram should balance technical depth with clarity. Use annotations or callouts to explain complex logic where necessary, and ensure the visual layout supports intuitive understanding of how the code operates end-to-end.



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
