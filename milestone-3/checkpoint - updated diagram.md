# Process Design Document (PDD) - Working Draft
**Team Name:** Group 2
**Project Title:** Personal Networking Outreach Assistant 
**Current Phase:** Week 4 (Advanced Logic Design)

---

## Part 1: Process Mapping (The "As-Is" State)

#### https://github.com/msacouto-ffld/data6900-group-project/blob/main/milestone-1/pdd-v2.md
---
## [Part 2: The Core Capability (The Linear Worker)]
#### https://github.com/msacouto-ffld/data6900-group-project/blob/main/milestone-2/MVW.md
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
flowchart TD

    %% ── ENTRY ──────────────────────────────────────────────
    START([⚡ Job Posting]) --> B1

    %% ══════════════════════════════════════════════════════
    %% STEP B — Identify Company + Job Title + Background
    %% ══════════════════════════════════════════════════════

    B1[🤖 B1 Gatekeeper: Structured Job Extraction]
    B1 --> B2[⚖️ B2 Judge: Search Parameter Reasoning]

    B2 --> B_CRITIC[🔍 B2 Critic: Title Realism + Anchor Discipline Audit]
    B_CRITIC --> B_LOOP{Are Titles Market-Realistic\nAND Is Primary Company Anchor Dominant?}

    B_LOOP -- No: Rare Titles / Anchor Drift / Over-Broad Scope --> B2
    B_LOOP -- Yes: Realistic Titles + Clear Primary Anchor --> B_ROUTER{Does Job Include Strong Company Signal\nAND Valid University Match?}

    B_ROUTER -- Yes: Strong Anchor Signals Present --> B3_A[✍️ B3 Worker: Anchor-First Query (Company Locked + Titles)]
    B_ROUTER -- No: Weak Anchor Signals --> B3_B[✍️ B3 Worker: Skill-Weighted Query (Titles + Core Skills Only)]

    B3_A --> C1
    B3_B --> C1

    %% ══════════════════════════════════════════════════════
    %% STEP C — Analyze Profiles for Relevance
    %% ══════════════════════════════════════════════════════

    C1[🤖 C1 Gatekeeper: Profile Extraction (Strictly Profile-Bound)]
    C1 --> C_ROUTER{Are Core Fields Present\n(Name, Role, Company)\nAND No Hallucinated Skills?}

    C_ROUTER -- No: Missing Core Data / Tool Over-Extraction --> C1_FALLBACK[🔄 C1 Fallback: Re-Extract with Null Enforcement + Tool Filtering]
    C1_FALLBACK --> C2
    C_ROUTER -- Yes: Clean Structured JSON --> C2

    C2[⚖️ C2 Judge: Calibrated Relevance Scoring]

    C2 --> C_CRITIC[🔍 C2 Critic: Precision Threshold + Inflation Check]
    C_CRITIC --> C_LOOP{Is "High" Tier Reserved for\nStrong Multi-Signal Alignment?}

    C_LOOP -- No: Over-Assigned High / Flat Tiering --> C2
    C_LOOP -- Yes: Clear Tier Separation + Ranking --> C3[✍️ C3 Worker: Structured Lead Summary\n(Core Competency ≠ Tools)]

    %% ══════════════════════════════════════════════════════
    %% STEP D — Draft Customized Message
    %% ══════════════════════════════════════════════════════

    C3 --> D_ROUTER{Are Strong Personalization Anchors Identified\n(Role Match, Company Match, Skill Overlap)?}

    D_ROUTER -- No: Weak or Generic Anchors Selected --> D1_FALLBACK[🔄 D1 Fallback: Re-Rank Anchors by Strength]
    D_ROUTER -- Yes: High-Signal Anchors Confirmed --> D2

    D1_FALLBACK --> D2

    D2[⚖️ D2 Judge: Personalization Strategy (Tone + Priority Order)]
    D2 --> D3[✍️ D3 Worker: Draft Message]

    D3 --> D_CRITIC[🔍 D3 Critic: Tone Calibration + Length + Explicit CTA Audit]
    D_CRITIC --> D_LOOP{Professional Tone?\nConcise Length?\nClear Actionable Ask with Time Horizon?}

    D_LOOP -- No: Overconfident / Too Long / No Clear Ask --> D3
    D_LOOP -- Yes: Calibrated Tone + Specific CTA --> HUMAN

    %% ── EXIT ──────────────────────────────────────────────
    HUMAN([🛠️ Human Review & Send])

    %% ══════════════════════════════════════════════════════
    %% STYLING
    %% ══════════════════════════════════════════════════════

    %% Week 3 nodes — Orange
    style B1 fill:#FFF4DD,stroke:#E0C070
    style B2 fill:#FFF4DD,stroke:#E0C070
    style B3_A fill:#FFF4DD,stroke:#E0C070
    style B3_B fill:#FFF4DD,stroke:#E0C070
    style C1 fill:#FFF4DD,stroke:#E0C070
    style C2 fill:#FFF4DD,stroke:#E0C070
    style C3 fill:#FFF4DD,stroke:#E0C070
    style D2 fill:#FFF4DD,stroke:#E0C070
    style D3 fill:#FFF4DD,stroke:#E0C070

    %% Router nodes — Green
    style B_ROUTER fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style C_ROUTER fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D_ROUTER fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px

    %% Critic nodes — Green
    style B_CRITIC fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style C_CRITIC fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D_CRITIC fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px

    %% Fallback nodes — Green
    style C1_FALLBACK fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D1_FALLBACK fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
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

Starting with the highest-risk failure node first (D1 silent corruption), then working through the approved pattern assignments.

#### **[Module A: Query Construction Router]**

```
Input Variable: {C3_lead_summary} — plain text lead summary produced by C3 Worker
| Category   | Condition                                                                                                   | Next Step                                                                                  |
|------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| VALID      | All six fields present and profile-sourced (name, company, role, skills, interests, university)            | Pass directly to **D2 Judge**                                                               |
| CORRUPTED  | Any field contains inferred, rewritten, or hallucinated values not traceable to C3 output                  | Route to **D1 Fallback re-parse**                                                           |
| INCOMPLETE | One or more fields missing or null                                                                          | Route to **D1 Fallback re-parse** with strict null rules                                    |
```

```
RAFT Prompt:
#### Role
Router AI: Field Integrity Validator for Message Drafting Input

#### Audience
Machine (routing decision only — no human output)

#### Format
JSON:
{
  "status": "VALID" | "CORRUPTED" | "INCOMPLETE",
  "failed_fields": [] | ["skills", "interests", ...],
  "reason": ""
}

#### Task
- Receive the plain text lead summary from Step C.
- Verify that all six fields are present and traceable to the summary:
  name, current_company, current_role, skills, interests, university.
- For each field, ask internally:
  "Does this value appear explicitly in the C3 summary — or was it inferred?"
- If all fields are present and traceable: output status VALID.
- If any field contains values not present in the C3 summary: output status CORRUPTED
  and list the affected fields in failed_fields.
- If any field is missing or empty: output status INCOMPLETE
  and list the affected fields in failed_fields.
- Do NOT attempt to fix or fill missing fields.
- Do NOT pass judgment on relevance or message quality.
- Output routing decision only.
```

#### **[Next Module]
  

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

### 3.6 Claude logs:
#### https://claude.ai/share/6cbc5360-62ad-41d2-ae1e-b333838db0aa
#### https://claude.ai/share/130e5ea6-54e9-4304-bae9-15071cf22a2d
