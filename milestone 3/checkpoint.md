# Process Design Document (PDD) - Working Draft
**Team Name:**
**Project Title:**
**Current Phase:** Week 4 (Advanced Logic Design)

> *This version assumes you already completed the week 2 and week 3 portions. Copy them in the respective sections.*
---

## [Part 1: Process Analysis]
*(Retain your Week 2 content: As-Is Map, Business Case, etc.)*

---

## [Part 2: The Core Capability (The Linear Worker)]
*(Retain your Week 3 content. This Linear Chain (Gatekeeper -> Judge -> Worker) will likely become one of the "Branches" in your new system.)*

---

## Part 3: The Intelligent Network (Week 4 Additions)

*In Week 4, we wrap the Linear Core in advanced logic to handle variety (Routing) and quality (Looping).*

### 3.1 The Architecture Strategy
*Which Advanced Patterns are you deploying to fix the "Real World Complexity"? Check at least one.*
*   [X] **The Router (Branching):** To handle different types of inputs (e.g., separating Spam from Valid Requests).
*   [X] **The Evaluator-Optimizer (Looping):** To ensure quality/safety (e.g., checking the Draft before sending).
*   [ ] **The Orchestrator-Workers (Parallel):** To handle complex, multi-step research.

### 3.2 The Advanced Logic Map (Mermaid)
*(Update your diagram. It should now contain Diamonds (Decisions) or Circles (Loops) wrapping around your nodes.)*

```mermaid

```

### 3.3 The Orchestrator Logic
*Define the step-by-step execution plan (The "Operating System"). This replaces the simple "1-2-3" sequence.*

#### WORKFLOW VARIABLES
```
# Inputs


# Gatekeeper outputs


# Judge outputs


# Critic outputs

```

#### WORKFLOW CONDITIONS
##### Router (Pre-Gatekeeper)
```

```

##### Critic (Post-Judge Evaluator Loop)
```
# Initialize loop


    # Feedback to Judge
    
```

---

### 3.4 New Component Definitions (The Modules)
*Define the Specs and Prompts for the NEW tools you added (Router or Critic). You do not need to redefine the tools from Part 2.*

#### **[Module A: The Router Configuration]**

**Tool Name:** Input Qualification Router
  *   **Input Variable:**
      *   `{{transcript}}` (String), `{{vendor_csv}}` (String)
  *   **Output Categories:** (What are the specific pass/fail criteria?)
      *   VALID
        * Required financial facts are explicitly present in authoritative sources (CSV preferred).
        * Numeric values are concrete (no hedging language).
      * AMBIGUOUS
        * Required facts exist but are vague, approximate, or transcript-only.
        * Extraction is possible only with forced inference flags.
      * INSUFFICIENT
        * One or more mandatory fields cannot be grounded in any source.
        * Downstream automation must fail closed or escalate.
  *   **R.A.F.T. Prompt Draft:**
      ```
      # Role
      
      # Audience

      
      # Format
     
      
      # Task
     
      
     
      
      # Rules
    
      ```

#### **[Module B: The Evaluator Configuration]**

*   **Tool Name:** Judge Critic / Evaluator Loop (NEW)
*   **Input Variable:** 
    * {{judge_xml_output}} (XML)
      * <thinking>: Step-by-step reasoning
      * <verdict>: Proposed decision (APPROVE or REJECT)
    * {{gatekeeper_json_output}} (JSON)
      * Structured financial facts, including inferred flags
*   **Evaluation Rubric:** (What are the specific pass/fail criteria?)
    | Rule                                    | Description                                                                                                      |
    | :-------------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
    | **Mandatory Fields Present**            | All critical fields (`requested_shift_amount`, `target_line_item`, `current_overhead_reference`) must exist.     |
    | **No Over-Confidence on Inferred Data** | Fields marked `"inferred": true` must trigger a conditional or REJECT verdict if they are critical for approval. |
    | **Budget Limit Enforcement**            | Requested shift must not exceed $10,000.                                                                         |
    | **MSA Trigger Rule**                    | Any shift > $5,000 must trigger MSA check.                                                                       |
    | **Overhead Qualification**              | `target_line_item` must have a validated overhead classification.                                                |
    | **Fail-Closed Principle**               | If any precondition fails, the final verdict is downgraded to REJECT or NEEDS REVIEW.                            |

*   **R.A.F.T. Prompt Draft:**
    ```
    # Role
    
    # Audience
 
    
    # Format
    
    # Task

    
    # Rules

    ```
  

---

### 3.5 Advanced Simulation Log (Proof of Robustness)
*Provide a chat log showing the Logic handling a complex case.*

**Scenario: The Edge Case**
*   **Input:** 
  ```
  
  ```
*   **Trace:**
  ```
  *
  ```
* **Observations from Simulation**
  * 
