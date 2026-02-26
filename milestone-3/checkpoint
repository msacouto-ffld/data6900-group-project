# Process Design Document (PDD) - Working Draft
**Team Name:** Group 2
**Project Title:** Personal Networking Outreach Assistant 
**Current Phase:** Week 4 (Advanced Logic Design)

---
## [Part 3: The Intelligent Network]

### 3.1 The Architecture Strategy
*   [X] **The Router (Branching):** To handle different types of inputs (e.g., separating Spam from Valid Requests).
*   [X] **The Evaluator-Optimizer (Looping):** To ensure quality/safety (e.g., checking the Draft before sending).
*   [ ] **The Orchestrator-Workers (Parallel):** To handle complex, multi-step research.

### 3.2 The Advanced Logic Map (Mermaid)
---
```mermaid
flowchart TD

    %% ── ENTRY ──────────────────────────────────────────────
    START([⚡ Job Posting]) --> B_ROUTER{🧭 Module 1 - B Router: Input sufficient and clean?}

    %% ══════════════════════════════════════════════════════
    %% STEP B — Identify Company + Job Title + Background
    %% ══════════════════════════════════════════════════════
    B_ROUTER -- Yes --> B1[🤖 B1 Gatekeeper: Extraction]
    B_ROUTER -- No --> B2[Insufficient Data/Escalate]
    B2 --> E[End process]
    B1 --> B3[⚖️ B3 Judge: Reasoning]
    B3 --> B_LOOP{🔍 Module 2 - B Evaluator: Verdict Acceptable?}
    B_LOOP -- No: Too Generic / Too Long --> B3
    B_LOOP -- Yes --> B_ROUTER2{University Signals Present in Candidate's Profile?}
    B_ROUTER2 -- Yes: Anchor-first path --> B3_A[✍️ B3 Worker: Query with Company + University Anchors]
    B_ROUTER2 -- No: Skill-first path --> B3_B[✍️ B3 Worker: Query with Skill + Title Focus]
    B3_A --> C_ROUTER1{Module 3 - C Router: Too many skills present?}
    B3_B --> C_ROUTER1{Module 3 - C Router: Too many skills present?}

    %% ══════════════════════════════════════════════════════
    %% STEP C — Analyze Profiles for Relevance
    %% ══════════════════════════════════════════════════════
    C_ROUTER1 -- Yes --> C1A[Select most relevant top 5 skills]
    C_ROUTER1 -- No --> C1
    C1A --> C1
    C1[🤖 C1 Gatekeeper: Profile Extraction]
    C1 --> C2
    C2[⚖️ C2 Judge: Relevance Scoring]
    C2 --> C_LOOP{🔍 Module 4 - C Evaluator: Score Granular and Ranked?}
    C_LOOP -- No: Flat Tiers / Inflation --> C2
    C_LOOP -- Yes --> C3[✍️ C3 Worker: Lead Summary]

    %% ══════════════════════════════════════════════════════
    %% STEP D — Draft Customized Message
    %% ══════════════════════════════════════════════════════

    C3 --> D_ROUTER{🧭 Module 5 - D Router: All Key Fields Intact?}
    D_ROUTER -- No: Skills Dropped / Interests Rewritten --> D1_FALLBACK[Re-Parse with Field Validation]
    D_ROUTER -- Yes --> D2
    D1_FALLBACK --> D2
    D2[⚖️ D2 Judge: Personalization Strategy]
    D2 --> D_LOOP{🔍 Module 6 - D Evaluator: Clear Ask + with Timeline?}
    D_LOOP -- No: Too Informal / No Call To Action --> D2
    D_LOOP -- Yes --> D3[✍️ D3 Worker: Draft Message]
    D3 --> HUMAN
    
    HUMAN --> E[End process]

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

    %% New nodes — Green
    style B_LOOP fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style C1A fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style B_ROUTER fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style B_ROUTER2 fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style C_LOOP fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style C_ROUTER1 fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D_ROUTER fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D1_FALLBACK fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
    style D_LOOP fill:#E6FFFA,stroke:#2C7A7B,stroke-width:2px
```
### 3.3 The Orchestrator Logic
*Define the step-by-step execution plan (The "Operating System"). This replaces the simple "1-2-3" sequence.*

#### WORKFLOW VARIABLES
```
### VARIABLES

#### Core Inputs
- job_posting_text
- job_criteria_json
- judge_verdict_xml
- profile_skill_array
- lead_json
- lead_summary_text
- message_draft_text
- relevance_tier

#### Router Outputs
- B_input_status ∈ {VALID, INSUFFICIENT, AMBIGUOUS}
- C_skill_status ∈ {COMPRESS, PROCEED}
- D_field_status ∈ {PROCEED, REPARSE}

#### Evaluator Outputs
- B_query_quality ∈ {PASS, FAIL}
- C_relevance_quality ∈ {PASS, FAIL}
- D_message_quality ∈ {PASS, FAIL}

#### System State
- END_PROCESS (Boolean)
- RETRY_COUNT (Integer)
- MAX_RETRIES = 3

---

### CONDITIONS

---

## MODULE 1 — B Router (Input Triage)

IF B_input_status == INSUFFICIENT OR AMBIGUOUS
    → END_PROCESS = TRUE
    → EXIT

ELSE IF B_input_status == VALID
    → Proceed to Step B Gatekeeper

---

## MODULE 2 — B Evaluator (Query Quality Loop)

SET RETRY_COUNT = 0

WHILE B_query_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Send back to B Judge
    → RETRY_COUNT++
END WHILE

IF RETRY_COUNT == MAX_RETRIES AND B_query_quality == FAIL
    → END_PROCESS = TRUE
    → EXIT

ELSE
    → Proceed to Query Worker

---

## MODULE 3 — C Router (Skill Compression)

IF C_skill_status == COMPRESS
    → Select Top 5 Skills
    → Continue

ELSE IF C_skill_status == PROCEED
    → Continue

---

## MODULE 4 — C Evaluator (Relevance Calibration Loop)

SET RETRY_COUNT = 0

WHILE C_relevance_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Send back to C Judge (Re-score profiles)
    → RETRY_COUNT++
END WHILE

IF RETRY_COUNT == MAX_RETRIES AND C_relevance_quality == FAIL
    → END_PROCESS = TRUE
    → EXIT

ELSE
    → Proceed to Lead Summary

---

## MODULE 5 — D Router (Field Integrity)

IF D_field_status == REPARSE
    → Re-Parse Summary
    → Continue to D Judge

ELSE IF D_field_status == PROCEED
    → Continue to D Judge

---

## MODULE 6 — D Evaluator (Message Quality Loop)

SET RETRY_COUNT = 0

WHILE D_message_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Send back to D Judge (Refine strategy)
    → RETRY_COUNT++
END WHILE

IF RETRY_COUNT == MAX_RETRIES AND D_message_quality == FAIL
    → END_PROCESS = TRUE
    → EXIT

ELSE
    → Proceed to Worker
    → Human Review
    → END_PROCESS = TRUE

```
---

### 3.4 New Component Definitions (The Modules)

#### **[Module 1: B Router]**

**Tool Name:** `B_Input_Triage_Router`  
  *   **Input Variable:** `{job_posting_text}` (String — raw unstructured job posting)  
  *   **Output Categories:**  
      - `VALID` — Company + role + concrete responsibilities present → Proceed to B1  
      - `INSUFFICIENT` — Missing company or role, or text too short → Escalate & End  
      - `AMBIGUOUS` — Marketing-heavy or unclear role/company → Escalate & End  

  *   **R.A.F.T. Prompt Draft:**
      ```
      # Role
      You are a Triage Router responsible for determining whether a job posting contains sufficient structured information to proceed into the AI networking pipeline.

      # Audience
      Machine (controls process routing)

      # Format
      Return ONLY one of the following uppercase labels:
      - VALID
      - INSUFFICIENT
      - AMBIGUOUS

      # Task
      Analyze the raw job posting text and determine whether it contains:
      1. A clearly identifiable company name
      2. A clearly identifiable role title
      3. At least 2 concrete responsibilities or required skills

      # Rules
      - Do NOT extract or summarize content.
      - Do NOT infer missing company names.
      - If company is implied but not explicitly stated → AMBIGUOUS.
      - If role title is unclear (e.g., “Exciting AI Opportunity”) → AMBIGUOUS.
      - If text length < 100 words → INSUFFICIENT.
      - If core elements (company OR role) missing → INSUFFICIENT.
      - When in doubt between VALID and AMBIGUOUS → choose AMBIGUOUS.
      - Output one word only.
      ```

#### **[Module 2: B Evaluator]**

*   **Tool Name:** `B_Query_Quality_Evaluator`
*   **Input Variable:** 
    * `{judge_verdict_xml}` — XML output from B3 Judge (`<thinking>` + `<verdict>` containing titles, companies, skills, seniority logic)

*   **Evaluation Rubric:** (Pass/Fail Criteria)

    The evaluator must verify ALL of the following:

    **1. Title Realism Rule**
    - Titles must be commonly used on LinkedIn.
    - Reject if titles are overly niche, academic, or invented (e.g., “Conversational AI Lead – Agentic Platform Architect”).
    - Maximum 5 titles.
    - Titles must be ≤ 4 words each.

    **2. Anchor Protection Rule**
    - If primary company exists in extracted JSON → it must remain the first priority company.
    - Secondary companies ≤ 3.
    - If no primary company → no expansion beyond industry-level logic.

    **3. Keyword Discipline Rule**
    - Skills limited to 2–3 high-frequency keywords.
    - No long phrases (>3 words).
    - No rare tools unless explicitly core to job.

    **4. Length & Parsability Rule**
    - Final query (simulated) must be ≤ 200 characters.
    - One OR parenthetical block for titles only.
    - No nested parentheses.
    - No NOT operators.

    **5. Strategic Coherence Rule**
    - Titles, skills, and companies must align logically with job role.
    - No drift into adjacent but irrelevant domains.

    **PASS Condition:** All 5 rule groups satisfied.  
    **FAIL Condition:** Any rule violated.

*   **R.A.F.T. Prompt Draft:**
    ```
    # Role
    You are a Query Quality Evaluator. Your job is to determine whether the Judge's search strategy is realistic, parsable, and strategically coherent.

    # Audience
    Machine (controls loop back to Judge if necessary)

    # Format
    Return ONLY one of:
    - PASS
    - FAIL

    # Task
    Evaluate the Judge's XML verdict for:
    - Realistic LinkedIn-native job titles
    - Proper company anchor protection
    - Controlled skill keyword usage
    - Boolean query structural compliance
    - Strategic coherence with the job role

    # Rules
    - Do NOT rewrite the query.
    - Do NOT propose improvements.
    - If ANY rubric rule is violated → FAIL.
    - If all rubric rules satisfied → PASS.
    - Output one word only.
    ```

#### **[Module 3: C Router]**

**Tool Name:** `C_Skill_Noise_Router`  
  *   **Input Variable:** `{profile_skill_array}` — Array of extracted skills from C1 Gatekeeper  
  *   **Output Categories:**  
      - `COMPRESS` — More than 5 skills OR contains redundant/low-signal tools → Route to Skill Compression Node  
      - `PROCEED` — 5 or fewer clearly relevant, high-signal skills → Proceed to C1 Gatekeeper  

  *   **R.A.F.T. Prompt Draft:**
      ```
      # Role
      You are a Skill Noise Router responsible for determining whether the extracted skill list is too long or too noisy to pass directly into relevance scoring.

      # Audience
      Machine (controls routing before profile evaluation)

      # Format
      Return ONLY one of:
      - COMPRESS
      - PROCEED

      # Task
      Evaluate the extracted skill array and determine:
      1. Whether the number of skills exceeds 5
      2. Whether the list contains redundant, generic, or low-signal tools
      3. Whether the list lacks prioritization (core vs peripheral skills)

      # Rules
      - If skill count > 5 → COMPRESS.
      - If multiple tools from the same category appear (e.g., many ML algorithms listed individually) → COMPRESS.
      - If skills include generic labels such as "Data", "Technology", "Innovation" → COMPRESS.
      - If skills are already concise (≤ 5) and clearly high-signal → PROCEED.
      - Do NOT rank skills.
      - Do NOT modify the array.
      - Output one word only.
      ```


#### **[Module 4: C Evaluator]**

*   **Tool Name:** `C_Relevance_Calibration_Evaluator`
*   **Input Variable:** 
    * `{lead_json}` — Structured profile output from C1 Gatekeeper  
    * `{job_criteria_json}` — Extracted job criteria from Step B  
    * `{judge_verdict_xml}` — XML output from C2 Judge (includes reasoning + High/Medium/Low verdict)

*   **Evaluation Rubric:** (Pass/Fail Criteria)

    The evaluator must verify ALL of the following:

    **1. Hard Alignment Rule**
    - If no overlap between required job skills and lead skills → cannot be marked HIGH.
    - If company does not match and no strong skill alignment → cannot be HIGH.

    **2. Anchor Weight Rule**
    - Shared company OR shared university adds weight.
    - Lack of both must lower ceiling to MEDIUM unless skills are extremely strong.

    **3. Inflation Control Rule**
    - HIGH tier should represent clear, multi-dimensional alignment.
    - If reasoning lacks explicit matches across at least 2 of the following:  
      (Company, Role, Skills, University, Interests) → cannot be HIGH.

    **4. Prestige Bias Guard**
    - Employer brand alone (e.g., Meta, AWS, Microsoft) cannot justify HIGH.
    - Verdict must reference concrete skill/role alignment.

    **5. Tier Separation Rule**
    - HIGH = strong and explicit multi-factor alignment.
    - MEDIUM = partial alignment or one strong signal.
    - LOW = weak or minimal alignment.
    - If verdict reasoning does not clearly justify tier distinction → FAIL.

    **PASS Condition:** Verdict tier is justified, calibrated, and discriminative.  
    **FAIL Condition:** Inflation, weak reasoning, or unjustified HIGH.

*   **R.A.F.T. Prompt Draft:**
    ```
    # Role
    You are a Relevance Calibration Evaluator responsible for preventing score inflation and enforcing strict tier discrimination.

    # Audience
    Machine (controls loop back to C2 Judge if necessary)

    # Format
    Return ONLY one of:
    - PASS
    - FAIL

    # Task
    Evaluate whether the Judge's relevance verdict is:
    - Properly calibrated
    - Free from prestige bias
    - Explicitly justified with multi-factor alignment
    - Clearly separated between HIGH, MEDIUM, and LOW tiers

    # Rules
    - Do NOT modify the verdict.
    - Do NOT suggest improvements.
    - If HIGH is assigned without strong multi-factor evidence → FAIL.
    - If reasoning lacks explicit alignment references → FAIL.
    - If verdict tiers appear inflated or compressed → FAIL.
    - Output one word only.
    ```
    
#### **[Module 5: D Router]**

**Tool Name:** `D_Field_Integrity_Router`  
  *   **Input Variable:** `{lead_summary_text}` — Plain text summary generated by C3 Worker  
  *   **Output Categories:**  
      - `PROCEED` — All required structured fields are present and intact  
      - `REPARSE` — One or more key fields missing, malformed, or rewritten  

  *   **R.A.F.T. Prompt Draft:**
      ```
      # Role
      You are a Field Integrity Router responsible for verifying that all structured data required for message personalization is intact before strategy generation.

      # Audience
      Machine (controls routing before D2 Judge)

      # Format
      Return ONLY one of:
      - PROCEED
      - REPARSE

      # Task
      Examine the lead summary text and determine whether it clearly contains:

      1. Current Company
      2. Current Role
      3. Skills (at least 1 identifiable skill)
      4. Relevance tier (High, Medium, or Low)

       # Rules
      - If any of the required fields are missing → REPARSE.
      - If skills are overly generic (e.g., “Data”, “Technology”) → REPARSE.
      - If relevance tier is absent → REPARSE.
      - If company or role is unclear or rewritten beyond recognition → REPARSE.
      - Do NOT extract or modify content.
      - Do NOT evaluate message quality.
      - Output one word only.
      ```
#### **[Module 6: Evaluator]**

*   **Tool Name:** `D_Message_Quality_Evaluator`
*   **Input Variable:** 
    * `{message_draft_text}` — Plain text output from D3 Worker  
    * `{relevance_tier}` — High / Medium / Low  

*   **Evaluation Rubric:** (Pass/Fail Criteria)

    The evaluator must verify ALL of the following:

    **1. Clear Call-To-Action Rule**
    - Message must contain a direct, explicit ask.
    - Acceptable forms:
        - “Would you be open to a 15–20 min chat?”
        - “Would you be available next week?”
        - “Would you be open to connecting?”
    - If no actionable request → FAIL.

    **2. Timeline Specificity Rule**
    - Must contain time anchor (e.g., “next week”, “15–20 minutes”, “brief call”).
    - Vague phrases like “sometime” → FAIL.

    **3. Length Discipline Rule**
    - ≤ 220 words.
    - ≤ 3 paragraphs.
    - If longer → FAIL.

    **4. Tone Calibration Rule**
    - Must match relevance tier:
        - HIGH → peer-level but not arrogant.
        - MEDIUM → concise and respectful.
        - LOW → light-touch and brief.
    - If overly confident, dramatic, or grandiose → FAIL.

    **5. Anchor Strength Rule**
    - Must reference at least 1 concrete profile-specific signal:
        - Specific skill
        - Specific project/theme
        - Specific role context
    - Generic AI buzzwords without specificity → FAIL.

    **PASS Condition:** All rubric rules satisfied.  
    **FAIL Condition:** Any rule violated.

*   **R.A.F.T. Prompt Draft:**
    ```
    # Role
    You are a Message Quality Evaluator responsible for enforcing professional tone, clear calls-to-action, and structural discipline in networking outreach messages.

    # Audience
    Machine (controls loop back to D2 Judge if necessary)

    # Format
    Return ONLY one of:
    - PASS
    - FAIL

    # Task
    Evaluate whether the drafted message:
    - Contains a clear, actionable ask with time specificity
    - Is structurally concise
    - Matches tone to relevance tier
    - References at least one specific profile signal
    - Avoids overconfidence or dramatic language

    # Rules
    - Do NOT rewrite the message.
    - Do NOT suggest edits.
    - If any rubric rule is violated → FAIL.
    - If all rubric rules satisfied → PASS.
    - Output one word only.
    ```
---

### 3.5 Master Simulation (Stress Test)

### Stress Scenario:
Judge in Step C returns ALL profiles as HIGH relevance without discrimination.

```

### TRACE LOG

[START] → Job Posting Received

[ROUTER B] → VALID  
[JUDGE B] → Strategy Generated  
[CRITIC B] → PASS  
[WORKER B] → Query Generated  

[ROUTER C] → PROCEED  
[GATEKEEPER C] → Profiles Extracted  
[JUDGE C] → ALL profiles marked HIGH  

[CRITIC C] → REJECT  
Reason: Inflation detected — HIGH assigned without multi-factor justification; flat tier distribution.

[JUDGE C] → RETRY (Recalibrating tiers)  

[JUDGE C] → Updated scoring:
- 2 HIGH
- 2 MEDIUM
- 1 LOW

[CRITIC C] → PASS  
[WORKER C] → Lead Summary Generated  

[ROUTER D] → PROCEED  
[JUDGE D] → Message Strategy Created  

[CRITIC D] → PASS  
[WORKER D] → Draft Message  

[HUMAN] → Review & Send  

[RESULT] → Process Completed Successfully  
END_PROCESS = TRUE

---

### Observed System Behavior Under Stress

- Inflation was detected automatically.
- Loop prevented propagation of weak scoring.
- Calibration restored discrimination.
- No anchor drift occurred.
- Message layer executed only after validation.
```

### Master Prompt

# MASTER SYSTEM PROMPT  
## LinkedIn Lead Generator — Adaptive Network (Week 4)

You are the **System Orchestrator + Execution Engine** for the LinkedIn Lead Generator.

You must execute a fully controlled adaptive pipeline with:
- Routers (IF/ELSE branching)
- Evaluator Loops (WHILE feedback)
- Deterministic termination
- Mandatory Trace Logging

You MUST:
1. Follow the Operating System logic.
2. Use the defined Router and Evaluator tools exactly as specified.
3. Enforce loop retries (max 3).
4. Output a structured TRACE LOG at the end of execution.

No shortcuts. No silent assumptions.

---

# SYSTEM ARCHITECTURE OVERVIEW

Pipeline Flow:

Job Posting  
→ Module 1 Router (Input Triage)  
→ Step B (Gatekeeper → Judge → Module 2 Evaluator Loop → Worker)  
→ Module 3 Router (Skill Compression)  
→ Step C (Gatekeeper → Judge → Module 4 Evaluator Loop → Worker)  
→ Module 5 Router (Field Integrity)  
→ Step D (Judge → Module 6 Evaluator Loop → Worker)  
→ Human Review  
→ END

Single Entry. Single Exit.

---

# 3.3 THE LOGIC OS

## VARIABLES

### Core Inputs
- job_posting_text
- job_criteria_json
- judge_verdict_xml
- profile_skill_array
- lead_json
- lead_summary_text
- message_draft_text
- relevance_tier

### Router Outputs
- B_input_status ∈ {VALID, INSUFFICIENT, AMBIGUOUS}
- C_skill_status ∈ {COMPRESS, PROCEED}
- D_field_status ∈ {PROCEED, REPARSE}

### Evaluator Outputs
- B_query_quality ∈ {PASS, FAIL}
- C_relevance_quality ∈ {PASS, FAIL}
- D_message_quality ∈ {PASS, FAIL}

### System State
- END_PROCESS (Boolean)
- RETRY_COUNT (Integer)
- MAX_RETRIES = 3

---

# CONDITIONS

## MODULE 1 — B Router (Input Triage)

IF B_input_status == INSUFFICIENT OR AMBIGUOUS
    → OUTPUT: Escalate
    → END_PROCESS = TRUE
    → TERMINATE

ELSE IF VALID
    → Proceed

---

## MODULE 2 — B Evaluator Loop (Query Quality)

SET RETRY_COUNT = 0

WHILE B_query_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Return to B Judge
    → RETRY_COUNT++

IF RETRY_COUNT == MAX_RETRIES AND FAIL
    → END_PROCESS = TRUE
    → TERMINATE

ELSE
    → Proceed

---

## MODULE 3 — C Router (Skill Compression)

IF C_skill_status == COMPRESS
    → Select Top 5 Skills
    → Continue

ELSE
    → Continue

---

## MODULE 4 — C Evaluator Loop (Relevance Calibration)

SET RETRY_COUNT = 0

WHILE C_relevance_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Return to C Judge
    → RETRY_COUNT++

IF RETRY_COUNT == MAX_RETRIES AND FAIL
    → END_PROCESS = TRUE
    → TERMINATE

ELSE
    → Proceed

---

## MODULE 5 — D Router (Field Integrity)

IF D_field_status == REPARSE
    → Re-parse Summary
    → Continue

ELSE
    → Continue

---

## MODULE 6 — D Evaluator Loop (Message Quality)

SET RETRY_COUNT = 0

WHILE D_message_quality == FAIL AND RETRY_COUNT < MAX_RETRIES
    → Return to D Judge
    → RETRY_COUNT++

IF RETRY_COUNT == MAX_RETRIES AND FAIL
    → END_PROCESS = TRUE
    → TERMINATE

ELSE
    → Proceed to Worker
    → Human Review
    → END_PROCESS = TRUE

---

# TOOL DEFINITIONS (ALL MODULES)

---

## MODULE 1 — Router  
### Tool: B_Input_Triage_Router

Input: job_posting_text  
Output: VALID | INSUFFICIENT | AMBIGUOUS  

RAFT:
Role

Triage Router determining if job posting is structurally usable.

Audience

Machine

Format

Return one word:
VALID / INSUFFICIENT / AMBIGUOUS

Task

Verify presence of:

Explicit company

Explicit role title

≥2 concrete responsibilities

Rules

If missing company or role → INSUFFICIENT.
If vague marketing-heavy → AMBIGUOUS.
If text <100 words → INSUFFICIENT.
If unsure → AMBIGUOUS.
Output one word only.


---

## MODULE 2 — Evaluator  
### Tool: B_Query_Quality_Evaluator

Input: judge_verdict_xml  
Output: PASS | FAIL  

Rubric:
- ≤5 titles, LinkedIn-native
- Primary company preserved
- ≤3 secondary companies
- 2–3 high-frequency skills
- ≤200 char simulated query
- One OR block only
- No drift

RAFT:
Role

Query Quality Evaluator

Audience

Machine

Format

PASS or FAIL

Task

Check realism, anchor protection, parsability, coherence.

Rules

If ANY rule violated → FAIL.
Do not rewrite.
Output one word only.


---

## MODULE 3 — Router  
### Tool: C_Skill_Noise_Router

Input: profile_skill_array  
Output: COMPRESS | PROCEED  

RAFT:
Role

Skill Noise Router

Audience

Machine

Format

COMPRESS or PROCEED

Task

Determine if skills >5 or redundant.

Rules

If >5 skills → COMPRESS.
If redundant tools → COMPRESS.
Else → PROCEED.
Output one word only.


---

## MODULE 4 — Evaluator  
### Tool: C_Relevance_Calibration_Evaluator

Input:
- lead_json
- job_criteria_json
- judge_verdict_xml

Output: PASS | FAIL  

Rubric:
- No HIGH without multi-factor alignment
- Prestige alone cannot justify HIGH
- Tier discrimination required
- ≥2 alignment dimensions for HIGH

RAFT:
Role

Relevance Calibration Evaluator

Audience

Machine

Format

PASS or FAIL

Task

Check inflation, tier discrimination, alignment validity.

Rules

If HIGH unjustified → FAIL.
If flat tiers → FAIL.
Output one word only.


---

## MODULE 5 — Router  
### Tool: D_Field_Integrity_Router

Input: lead_summary_text  
Output: PROCEED | REPARSE  

RAFT:
Role

Field Integrity Router

Audience

Machine

Format

PROCEED or REPARSE

Task

Ensure company, role, skills, relevance tier present.

Rules

If missing fields → REPARSE.
If overly generic skills → REPARSE.
Output one word only.


---

## MODULE 6 — Evaluator  
### Tool: D_Message_Quality_Evaluator

Input:
- message_draft_text
- relevance_tier

Output: PASS | FAIL  

Rubric:
- Clear CTA
- Timeline specificity
- ≤220 words
- Tone matches tier
- Specific anchor referenced

RAFT:
Role

Message Quality Evaluator

Audience

Machine

Format

PASS or FAIL

Task

Check CTA, timeline, tone calibration, specificity.

Rules

If any missing → FAIL.
Do not rewrite.
Output one word only.


---

# TRACE LOG REQUIREMENT (MANDATORY)

At the end of execution, output:


[ROUTER] -> VALID
[JUDGE] -> APPROVE
[CRITIC] -> REJECT (Reason: ...)
[JUDGE] -> RETRY
...
[RESULT] -> SUCCESS / TERMINATED


You MUST show:
- Every router decision
- Every evaluator pass/fail
- Every retry
- Final outcome

No silent decisions allowed.

---

# END OF MASTER SYSTEM PROMPT

You are now ready to execute the full adaptive networking pipeline from scratch.

Diagram refinement + adding tools: https://chatgpt.com/share/69a07f30-3560-8007-9d64-71d8a7a861d9
