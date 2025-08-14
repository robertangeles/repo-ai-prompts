As a COBOL developer from the top 0.01%, you are helping a data engineering team reverse engineer undocumented Pro*COBOL batch programs. These programs read from flat files or source tables and write to relational database tables using embedded SQL. The goal is to rebuild the same logic in a modern data platform. The audience is a modern data engineer who does not know COBOL.

For the COBOL code I provide, return the following structured breakdown in clean Confluence ready format.

# SESSION
- Program: {{rehspabp.pco}}
- Lines in scope: {{1}}-{{3284}}
- Pass: {{Terrain}}  (Terrain | Inputs | Processing | Outputs | Prototype SQL | Mapping | Gaps | Lineage)
- Continuation: {{NEW}}
- Display the exact code in line {{1}} and line {{3284}}
- No Further Output Required


SECTION 1: PROGRAM OVERVIEW
- Scan the code from Line {{120}}-{{198}}
- Describe the overall purpose of the Pro COBOL Code in one or two sentences. 
- Display Summary Program Flow
- Return the entire response in Confluence ready format with clear headings. 

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

# SESSION
- Program: {{rehspabp.pco}}
- Lines in scope: {{1}}-{{3284}}
- Pass: {{Terrain}}  (Terrain | Inputs | Processing | Outputs | Prototype SQL | Mapping | Gaps | Lineage)
- Continuation: {{NEW}}
- Display the exact code in line {{1}} and line {{3284}}
- No Further Output Required

# I/O DIAGRAM
- Scan the code from Line {{208}}-{{3284}}
- Generate a comprehensive diagram illustrating the Input-Processing-Output (IPO) flow of the COBOL code.
- The diagram should clearly represent:
  - Inputs: Data sources, formats, and entry points.
  - Processing: Key logic, transformations, and decision points within the COBOL code.
  - Outputs: Final data structures, destinations, and formats.
- Format the Mermaid diagram with these **STRICT** requirements:
  - **MANDATORY: Use exactly these three subgraph names: INPUT, PROCESSING, OUTPUT**
  - Use explicit direction controls (direction TB/LR) within each subgraph
  - Keep node text brief (max 20 characters per line)
  - Use consistent connection style: ONLY `A --> B` format (no text on connections)
  - **Class definitions MUST follow these EXACT formatting rules:**
    - **Maximum 4 nodes per class definition line** (reduced from 6 for safety)
    - **Each class statement on exactly ONE line with NO line breaks**
    - **Format:** `class NODE1,NODE2,NODE3,NODE4 className`
    - **NO trailing spaces or commas after the last node**
    - **If more than 4 nodes needed, use multiple class lines**
    - **Node names must be ≤ 12 characters to prevent line overflow**
  - Use consistent node naming (alphanumeric + underscore only, no spaces or hyphens)
  - **MANDATORY: Validate total character count per class line ≤ 80 characters**
  - Maximum diagram complexity: 12 nodes total (4 per section - reduced for reliability)

## Required Diagram Structure:
```mermaid
graph TB
    subgraph INPUT ["INPUT"]
        direction TB
        [input nodes here - max 4]
    end

    subgraph PROCESSING ["PROCESSING"]
        direction TB
        [processing nodes here - max 4]
    end

    subgraph OUTPUT ["OUTPUT"]
        direction TB
        [output nodes here - max 4]
    end

    [connections between sections]

    classDef input fill:#e1f5fe,stroke:#01579b
    classDef process fill:#f3e5f5,stroke:#4a148c
    classDef output fill:#e8f5e8,stroke:#1b5e20

    class NODE1,NODE2,NODE3,NODE4 input
    class NODE5,NODE6,NODE7,NODE8 process
    class NODE9,NODE10,NODE11,NODE12 output
```
## MANDATORY Pre-Response Validation Checklist:
Before generating any Mermaid diagram, verify:
- [ ] **Syntax Check**: Manually verify each class definition follows exact format
- [ ] **Character Count**: Each class line ≤ 60 characters total
- [ ] **Node Count**: Maximum 4 nodes per class line
- [ ] **Node Existence**: All nodes in class definitions exist in diagram
- [ ] **Reserved Words**: No Mermaid reserved words as node names
- [ ] **Special Characters**: Only alphanumeric + underscore in node names
- [ ] **Line Termination**: Each statement properly terminated

## Built-in Validation Rules:
1. **Class Definition Pattern**: `^class [A-Z_,]{1,40} (input|process|output)$`
2. **Node Name Pattern**: `^[A-Z][A-Z0-9_]{1,11}$`
3. **Total Line Length**: `< 60 characters`
4. **Reserved Word Check**: Avoid: `graph`, `subgraph`, `direction`, `class`, `classDef`

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
