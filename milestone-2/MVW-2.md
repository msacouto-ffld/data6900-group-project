#  Process Design Document (PDD) - Milestone 2: MVW Design


### Process Design Document (PDD) - Phase 1 Complete
**Team Name:** Group #2

**Project Title:** LinkedIn Lead Generator

**Status:** Milestone 2 (Solution Design)

---

## [Part 1: Process Analysis]
# Process Design Document (PDD) - Milestone 1: Process Analysis
**Team Name:** Group 2
**Project Title:** LinkedIn Lead Generator
**Target Workflow:** Personal Daily Task

---

## Part 1: Process Mapping (The "As-Is" State)

### 1.1 The Scenario
A student wants to improve chances in the job market by manually generating leads on LinkedIn to connect with professionals who may provide referrals, insights, or interview opportunities. The process involves multiple manual steps, from identifying relevant profiles to drafting and sending personalized connection requests.

For each job posting, the student must extract key details, search for professionals at the company, evaluate their relevance, and write a customized message. Because personalization is required for every outreach attempt, the time required increases with the number of leads pursued.


### 1.2 The "As-Is" Diagram (Mermaid)

```mermaid
flowchart TD
    A[⚡ Job Posting] --> B[📦 Identify Company + Job Title + School/Common Background]
    B --> C[🛠️ Analyze Profile for Relevance; Pain Point: Time consuming]
    C --> D[🛠️ Draft Customized Message; Pain Point: Time consuming]
    D --> F[🛠️ Send Connection]

    %% Highlight the most time consuming bottlenecks (B, C, and D)
    style B fill:#f90
    style C fill:#f90
    style D fill:#f90
```

### 1.3 Pain Point Diagnosis
*   **The Bottleneck:** The main bottleneck occurs between "Identifying Company + Job Title + School/Common Background", “Analyze Profile” and “Draft Customized Message.” This stage requires reviewing unstructured profile information, exercising judgment about strategic value, and writing a personalized outreach message. It is the most cognitively demanding and time-intensive step, and it must be repeated for every potential connection.

*   **The Cost:** The student typically attempts 8–12 outreach connections per week. Profile analysis takes approximately 3–5 minutes per person, and drafting a customized message takes 7–10 minutes. This results in approximately 2–3 hours per week spent primarily on evaluation and message drafting, representing roughly 70–80% of total process time. Additional costs include cognitive fatigue, inconsistent message quality, and reduced outreach volume due to overthinking.

---

## Part 2: Opportunity Analysis (The Business Case)


### 2.1 The 3-Filter Analysis
| Activity                                                             | Pain (1-10) | Feasibility (1-10) | Risk (1-10) | Rationale                                                                                                       |
| -------------------------------------------------------------------- | ----------- | ------------------ | ----------- | --------------------------------------------------------------------------------------------------------------- |
| Evaluate profile for relevance                                       | 9           | 8                  | 4           | Requires interpreting unstructured profile information, identifying shared background, and judging strategic value. Highly repetitive and cognitively demanding. |
| Draft personalized message                                           | 9           | 8                  | 5           | Writing customized outreach is time-intensive and mentally taxing. Message quality directly impacts response rates. AI can generate strong drafts while preserving human review due to hallucination and tone ajustment risks.  |
| Search LinkedIn for relevant professionals                           | 7           | 8                  | 4           | Filtering by company, title, and shared background is structured and repeatable. AI can improve efficiency through ranking and prioritization. |
| Extract company + role + criteria from job posting                   | 6           | 9                  | 3           | Information extraction from job descriptions is well-suited for AI summarization and structured output generation. |
| Send connection request                                              | 4           | 9                  | 6           | Technically easy to automate, but full automation increases platform and account risk. Human control is preferred. |

### 2.2 The "Why AI?" Justification
| Activity                                           | Recommended Approach | Reasoning                                                                                                  |
| -------------------------------------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------- |
| Extract company + role + criteria                  | AI / Automation      | AI can quickly summarize job postings and extract structured information needed for targeting relevant professionals. |
| Search and rank relevant professionals             | AI / Automation      | AI can filter and prioritize candidates based on structured criteria such as company, role, and shared background. |
| Evaluate profile for relevance                     | AI-assisted (Hybrid) | AI can summarize profile highlights and identify alignment signals, reducing review time while allowing human validation. |
| Draft personalized message                         | AI-assisted (Hybrid) | AI can generate tailored draft messages using extracted profile data, reducing cognitive load and drafting time. Human review maintains authenticity. |
| Send connection request                            | Human                | Final sending remains human-controlled to reduce platform risk and ensure intentional outreach. |
---

## Part 3: Scope of Automation (The Setup for Week 3)


### 3.1 The Target Zone
From the AS-IS workflow, the Minimal Viable Workflow (MVW) we identified was:

Automate: Extract job criteria → Search and rank relevant professionals → Summarize profile highlights → Generate draft personalized message

Keep Human: Final evaluation of strategic fit → Final message edits → Sending connection requests

Summary Table:
| Step                                         | Current Responsibility | TO-BE Responsibility                |
| -------------------------------------------- | ---------------------- | ----------------------------------- |
| Extract company + role + criteria            | Human                  | AI                                  |
| Search for professionals                     | Human                  | AI-assisted                         |
| Evaluate profile for relevance               | Human                  | AI-assisted + Human validation      |
| Draft personalized message                   | Human                  | AI-assisted + Human refinement      |
| Send connection request                      | Human                  | Human                               |


### 3.2 The Hypothesis
*   By automating job criteria extraction, candidate filtering, and first-draft message generation, we expect to reduce the time spent on profile evaluation and drafting by approximately 50–70%. This would reduce total weekly effort from approximately 2–3 hours to approximately 1–1.5 hours per week, while maintaining or improving message quality and consistency through structured AI support and human review.

---

## Part 2: The "To-Be" Solution (Milestone 2)

### 2.1 The "To-Be" Map

```mermaid
graph TD
    A[⚡ LinkedIn Profiles Identified] --> B_subgraph
    B_subgraph --> H[👤 Human: Download PDFs & Upload to Gatekeeper]
    H --> D_subgraph
    D_subgraph --> F[🛠️ Human Review & Send]

    %% Automated AI Pipeline 1
    subgraph B_subgraph["Automated AI Pipeline: Identify Leads"]
        B1[🤖 Gatekeeper: Extract Company / Title / School / Skills] --> 
        B2[⚖️ Judge: Query Generating Strategies] --> 
        B3[✍️ Worker: Output LinkedIn Query]
    end

    %% Automated AI Pipeline 2
    subgraph D_subgraph["Automated AI Pipeline: Batch Extraction + Messaging"]
        D1[🤖 Gatekeeper: Extract Structured Leads JSON from PDFs] --> 
        D2[⚖️ Judge: Define Tone + CTA per Lead] --> 
        D3[✍️ Worker: Generate Personalized Messages]
    end

    %% Styling for AI nodes
    style B1 fill:#FFF4DD,stroke-dasharray:5 5
    style B2 fill:#FFF4DD,stroke-dasharray:5 5
    style B3 fill:#FFF4DD,stroke-dasharray:5 5

    style D1 fill:#FFF4DD,stroke-dasharray:5 5
    style D2 fill:#FFF4DD,stroke-dasharray:5 5
    style D3 fill:#FFF4DD,stroke-dasharray:5 5

    %% Styling for Human nodes
    style H fill:#E8F0FE
    style F fill:#E8F0FE
```
---

### 2.2 The R.A.F.T. Implementation (The Prompts)

**Automating Step B: Identify Company + Job Title + School/Common Background**

**Prompt 1 (Gatekeeper):**
```
#### Role
Gatekeeper AI: Structured Extractor for Search Strategy

#### Audience
Machine (downstream Judge node)

#### Format
JSON:
{
  "candidate": {
    "name": "",
    "university": "",
    "current_company": "",
    "current_role": "",
    "skills": []
  },
  "job": {
    "company": "",
    "role": "",
    "skills": []
  }
}

#### Task
- Receive:
    1. PDF of candidate LinkedIn profile
    2. Text of LinkedIn job posting
- Extract ONLY explicitly stated information.
- Do NOT infer missing values.
- If a field is not explicitly present, return null.
- Skills must be explicitly listed, not inferred.
- University must come from Education section only.
- Company must not confuse Education with Experience.
- Do NOT calculate years of experience.
- Do NOT infer seniority.

```
**Prompt 2 (Judge):**
```
#### Role  
Judge AI: Search Strategy Generator (State-Based)

#### Audience  
Machine (downstream Worker node)

#### Format  
XML with tags:  
<thinking> ... </thinking>  
<verdict> ... </verdict>  

---

#### Task  

You will receive structured JSON from the Gatekeeper with the following fields:

- candidate.university  
- job.company  
- job.role  

Your responsibility is to generate THREE deterministic search states.

You must NOT output Boolean queries.  
You must output structured anchor points and titles per state.

---

### Deterministic Title Logic

If job.role = "Data Scientist", use the following fixed title sets:

Primary Title Set:
- Data Scientist  
- Machine Learning Engineer  
- AI Engineer  

Broader Title Set:
- Senior Data Scientist  
- Data Science Manager  
- Machine Learning Specialist  

These title sets are fixed and must NOT be regenerated dynamically.

---

### Required States

STATE 1  
Anchors:
- Company = job.company  
- University = candidate.university  

Titles:
- Use the 3 Primary Title Set  

STATE 2  
Anchors:
- Company = job.company  
- University = candidate.university  

Titles:
- Use the 3 Broader Title Set  

STATE 3  
Anchors:
- Company = job.company  

Titles:
- Use the same 3 Broader Title Set (identical to State 2)

---

### Rules

- Always include candidate.university in State 1 and State 2.  
- Do NOT add anchors beyond company and university.  
- Exactly 3 titles per state.  
- Titles must be common LinkedIn titles (no niche variants).  
- Do NOT dynamically reinterpret the role.  
- Do NOT regenerate titles per retry.  
- Generate all 3 states in a single deterministic pass.

---

### Output Structure

<thinking>
- Identify extracted company
- Identify extracted university
- Confirm fixed primary title set
- Confirm fixed broader title set
</thinking>

<verdict>

STATE 1
Anchors:
- Company: {job.company}
- University: {candidate.university}

Titles:
- Data Scientist
- Machine Learning Engineer
- AI Engineer


STATE 2
Anchors:
- Company: {job.company}
- University: {candidate.university}

Titles:
- Senior Data Scientist
- Data Science Manager
- Machine Learning Specialist


STATE 3
Anchors:
- Company: {job.company}

Titles:
- Senior Data Scientist
- Data Science Manager
- Machine Learning Specialist

</verdict>
```
**Prompt 3 (Worker):**
```
#### Role
Worker AI: LinkedIn Query Renderer

#### Audience
Human (manual execution on LinkedIn)

#### Format
Plain Text

#### Task
- Receive one selected state from Judge.
- Render a single LinkedIn People keyword search string.

MANDATORY Constraints:
- ≤ 200 characters
- One parenthetical OR block (job titles only)
- Anchors placed outside parentheses
- No nested parentheses
- No NOT
- No explicit AND
- Use spaces as implicit AND

Output:
- One single line
- No explanations
- No labels
- No placeholders
```

**Automating Step D: Draft Customized Message**
**Prompt 1 (Gatekeeper):**
```
#### Role
Gatekeeper AI: Batch Profile Extractor

#### Audience
Machine (downstream Judge node)

#### Format
JSON:
{
  "leads": [
    {
      "name": "",
      "company": "",
      "role": "",
      "skills": [],
      "university": ""
    }
  ]
}

#### Task
- Receive 5 LinkedIn profile PDFs.
- Extract explicitly stated information only.
- Process all profiles in one batch.
- Each profile must be independent in structure.
- If a field is not present, return null.
- Do NOT infer interests.
- Do NOT calculate years of experience.
- Do NOT assign relevance.
- Strict profile-bound extraction.
```
**Prompt 2 (Judge):**
```
#### Role
Judge AI: Messaging Strategy Planner

#### Audience
Machine (downstream Worker node)

#### Format
XML with tags:
<thinking> ... </thinking>
<verdict> ... </verdict>

#### Task
- Receive batch JSON from Gatekeeper.
- Define a messaging strategy for each leads.

Rules:
- message must contain a specific call to action
- tone must be one of:
    "professional_peer"
    "warm_alumni"
    "curious_explorer"

- Do NOT rank leads.
- Do NOT evaluate relevance.


```
**Prompt 3 (Worker):**
```
#### Role
Worker AI: Personalized Message Generator

#### Audience
Human

#### Format
Plain Text

#### Task
- Receive:
    - JSON (leads array)
    - verdict from judge
- Generate 5 independent personalized messages.
- Loop internally over leads array.
- Each message must:
    - Reference fields according to priority_order
    - Apply selected tone
    - Avoid fabrications
    - Avoid referencing missing/null fields
- Messages must be clearly separated.
- Ready for human review.
```

---

### 2.3 The Tool Specifications (The Engineer's Audit)

## Step B | Tool A: Gatekeeper (Extraction)

**Goal:**  
Extract structured candidate + job data.

**Input Variables:**
- `{candidate_profile_pdf}`
- `{job_posting_text}`

**Output Schema:**
```json
{
  "candidate": {
    "name": "string | null",
    "university": "string | null",
    "current_company": "string | null",
    "current_role": "string | null",
    "skills": "array | null"
  },
  "job": {
    "company": "string | null",
    "role": "string | null",
    "skills": "array | null"
  }
}

Failure Mode:
If nothing extracted → return null across all fields.
```

## Step B | Tool B: Judge (Strategy Generator)

**Goal:**  
Precompute 3 deterministic query states.

**Input:**  
JSON from Tool A.

**Output:**  
3-state structured JSON.

**Constraints:**
- Exactly 3 titles per state.
- State 1 & 2 must include university anchor.
- State 3 drops university.
- No additional anchors.
- No inference beyond extracted data.

---

## Step B | Tool C: Worker (Query Rendering)

**Goal:**  
Render the ready-to-paste LinkedIn People Boolean query.

**Input:**  
Selected state JSON from Tool B (containing `anchors` and `titles`).

**Output:**  
Single-line LinkedIn People keyword search string (plain text).

**Output Requirements:**
- Exactly **one line**.
- No explanations.
- No labels.
- No placeholders.
- No line breaks.

**Structure Rules:**
- One parenthetical OR block for job titles only.
- Anchors (e.g., company, university) must appear outside parentheses.
- Anchors must be space-separated (implicit AND).

**Boolean Constraints:**
- ≤ 200 characters total.
- No nested parentheses.
- No `NOT`.
- No explicit `AND`.
- Use spaces as implicit AND.
- Only one OR block (for titles).

- 
# Step D | Tool A: Gatekeeper (Batch Extraction)

**Goal:**  
Extract structured data from 5 LinkedIn profile PDFs.

**Input:**  
`{5 profile PDFs}`

**Output Schema:**

```json
{
  "leads": [
    {
      "name": "string | null",
      "company": "string | null",
      "role": "string | null",
      "skills": "array | null",
      "university": "string | null"
    }
  ]
}

Rules:

Strictly extractive.

No inference.

No enrichment.

No relevance scoring.

Each lead must be independently structured.

If a field is not explicitly present → return null.

Do NOT calculate years of experience.

Do NOT infer interests.

Do NOT derive seniority.

Failure Mode:
If nothing extracted for a profile → return null across that profile’s fields.

## Step D | Tool B: Judge (Strategy Planner)

**Goal:**  
Define one shared messaging strategy to be applied uniformly across all 5 leads.

**Input:**  
`leads[]` JSON from Tool A.

**Output Schema:**
```json
{
  "{
  "message_strategy": {
    "ask": [],
    "tone": ""
  }
  }
}

Rules:

Define a strategy for each lead.

Do NOT rank leads.

Base strategy only on fields present in leads[].

"university"

"company"

"role"

"skills"

tone must be one of:

"professional_peer"

"warm_alumni"

"curious_explorer"

## Step D | Tool C: Worker (Message Drafting)

**Goal:**  
Generate 5 independent personalized outreach messages.

**Input:**  
- `leads[]` (JSON from Tool A)  
- `message_strategy` (JSON from Tool B)

**Output:**  
Plain text containing 5 clearly separated personalized messages.

---

### Behavioral Rules

- Generate exactly one message per lead.
- Internally iterate over the `leads[]` array.
- Apply the selected `tone` consistently in all messages.
- Reference only fields that are **not null**.
- Do NOT fabricate information.
- Do NOT infer missing data.
- Do NOT mention fields that are null.
- Do NOT include internal reasoning.

---

### Structural Rules

- Messages must be clearly separated (e.g., numbered or spaced).
- No JSON in the output.
- No explanations.
- No placeholders.
- No variable labels.
- Ready for human review and editing.

---

### Tone Guidance

- `professional_peer` → concise, respectful, direct.
- `warm_alumni` → friendly, connection-focused.
- `curious_explorer` → inquisitive, learning-oriented.

---

### Determinism Requirements

- Stateless rendering.
- No cross-profile contamination.
- No variation in tone between leads.
- Uniform application of the shared strategy.

---

### 2.4 "Proof of Life" (Simulation Log)

#### Step B
**Input:** 
`{{About the job About the role: Join our fast-growing Global Product Management Data Science team and help transform Gartner’s Client Experience Digital Platform—the essential destination for IT and business leaders worldwide. As a data scientist, you’ll leverage advanced analytics and machine learning to create intelligent, scalable solutions that deliver real value and enhance every step of our clients’ journey. In this role, you will lead complex data science projects in partnership with cross-functional teams, driving the development of advanced AI-powered chatbot systems that deliver intelligent, personalized experiences at scale. You’ll architect and implement cutting-edge conversational AI tools—including intelligent search, recommendation engines, and context-aware content systems—while ensuring seamless integration with enterprise platforms. What You Will Do Lead data science projects in close collaboration with Data Engineering, Application development, Product owners and business leaders to deliver high-value business capabilities Architect and build sophisticated AI-powered chatbot systems that provide intelligent, personalized client experiences at scale Design and implement advanced tools that power conversational AI capabilities, including intelligent search, recommendation engines, and context-aware content retrieval systems Design and implement Model Context Protocol (MCP) servers to enable seamless integration between AI agents, enterprise systems, and external tools Build user profiling and personalization models to deliver tailored chatbot experiences Be accountable for high-quality data science solutions with respect to accuracy, coverage, scalability, stability, and business adoption Take ownership of algorithms and drive enhancements/optimizations based on business requirements with proper documentation and code-reusability Leverage internal and external data to understand client's company-level priorities and deliver targeted support Collaborate with senior leadership on long-term vision, strategy, and solution roadmaps aligned with business objectives Pitch ideas, present solutions, and influence senior leaders and executive stakeholders with strong business value propositions Stay on top of fast-moving AI/ML models and technologies, particularly in LLMs, conversational AI, and agentic systems Collaborate with engineering and product teams to launch MVPs and iterate quickly Independently plan and drive complex data science projects that deliver measurable business value Mentor junior data scientists on chatbot development, LLM applications, and best practices What You Will Need 6-8 years hands-on experience building conversational AI systems, chatbots, LLM applications, or other advanced machine learning/artificial intelligence solutions to drive business impact Master's Degree or PhD in a quantitative field (math, computer science, engineering, etc.) required Strong communication skills in technical and business domains with demonstrated ability to translate quantitative analysis into actionable business strategies and influence executive leadership Working experience in some of the following data science areas: Large Language Models (LLMs) and Generative AI Conversational AI, chatbot development, and dialogue systems Natural Language Processing and text mining Search and Recommendation systems Prompt engineering, LLM fine-tuning, and model optimization AI agent architectures and orchestration Strong familiarity with Model Context Protocol (MCP) and building tools for AI agents Deep understanding of Lean product principles, software development lifecycle, and machine learning life cycle Practical, intuitive problem solver with proven ability to translate business objectives into actionable data science tasks and implement state-of-the-art ML research into production systems Experience and proficiency with Python, machine learning tools (e.g., scikit-learn, spacy, nltk), deep learning frameworks (e.g., pytorch, tensorflow, huggingface), LLM frameworks (e.g., LangChain, LlamaIndex), SQL/relational databases (e.g., Oracle), NoSQL databases (e.g., MongoDB, graph database), vector databases (e.g., Pinecone, Weaviate), distributed machine learning (spark), Linux and shell scripting Experience with cloud computing services such as AWS or Azure ML Strong ability to work collaboratively across product, data science and technical stakeholders with experience mentoring data scientists Ability to work in a culture that thrives on feedback and seeks opportunities to stretch outside comfort zone Bias for action and client outcome oriented What You Will Get Competitive salary, generous paid time off policy, charity match program, Group Medical Insurance, Parental Leave, Employee Assistance Program (EAP) and more! Collaborative, team-oriented culture that embraces diversity Professional development and unlimited growth opportunities Who are we? At Gartner, Inc. (NYSE:IT), we guide the leaders who shape the world. Our mission relies on expert analysis and bold ideas to deliver actionable, objective business and technology insights, helping enterprise leaders and their teams succeed with their mission-critical priorities. Since our founding in 1979, we’ve grown to 21,000 associates globally who support ~14,000 client enterprises in ~90 countries and territories. We do important, interesting and substantive work that matters. That’s why we hire associates with the intellectual curiosity, energy and drive to want to make a difference. The bar is unapologetically high. So is the impact you can have here. What makes Gartner a great place to work? Our vast, virtually untapped market potential offers limitless opportunities – opportunities that may not even exist right now – for you to grow professionally and flourish personally. How far you go is driven by your passion and performance. We hire remarkable people who collaborate and win as a team. Together, our singular, unifying goal is to deliver results for our clients. Our teams are inclusive and composed of individuals from different geographies, cultures, religions, ethnicities, races, genders, sexual orientations, abilities and generations. We invest in great leaders who bring out the best in you and the company, enabling us to multiply our impact and results. This is why, year after year, we are recognized worldwide as a great place to work. What do we offer? Gartner offers world-class benefits, highly competitive compensation and disproportionate rewards for top performers. In our hybrid work environment, we provide the flexibility and support for you to thrive — working virtually when it's productive to do so and getting together with colleagues in a vibrant community that is purposeful, engaging and inspiring. Ready to grow your career with Gartner? Join us. Gartner believes in fair and equitable pay. A reasonable estimate of the base salary range for this role is 113,000 USD - 147,000 USD. Please note that actual salaries may vary within the range, or be above or below the range, based on factors including, but not limited to, education, training, experience, professional achievement, business need, and location. In addition to base salary, employees will participate in either an annual bonus plan based on company and individual performance, or a role-based, uncapped sales incentive plan. Our talent acquisition team will provide the specific opportunity on our bonus or incentive programs to eligible candidates. We also offer market leading benefit programs including generous PTO, a 401k match up to $7,200 per year, the opportunity to purchase company stock at a discount, and more. The policy of Gartner is to provide equal employment opportunities to all applicants and employees without regard to race, color, creed, religion, sex, sexual orientation, gender identity, marital status, citizenship status, age, national origin, ancestry, disability, veteran status, or any other legally protected status and to seek to advance the principles of equal employment opportunity. Gartner is committed to being an Equal Opportunity Employer and offers opportunities to all job seekers, including job seekers with disabilities. If you are a qualified individual with a disability or a disabled veteran, you may request a reasonable accommodation if you are unable or limited in your ability to use or access the Company’s career webpage as a result of your disability. You may request reasonable accommodations by calling Human Resources at +1 (203) 964-0096 or by sending an email to ApplicantAccommodations@gartner.com. Job Requisition ID:106861 By submitting your information and application, you confirm that you have read and agree to the country or regional recruitment notice linked below applicable to your place of residence. Gartner Applicant Privacy Link: https://jobs.gartner.com/applicant-privacy-policy For efficient navigation through the application, please only use the back button within the application, not the back arrow within your browser.}}`

**Node 1 Output:**
```
{
  "candidate": {
    "name": "Margarida Martins Sacouto",
    "university": "Fairfield University",
    "current_company": "Fairfield University Charles F. Dolan School of Business",
    "current_role": "Graduate Assistant",
    "skills": [
      "AI Agents",
      "Sports Analytics",
      "Competitor Analysis"
    ]
  },
  "job": {
    "company": "Gartner",
    "role": "Data Scientist",
    "skills": [
      "Large Language Models (LLMs)",
      "Generative AI",
      "Conversational AI",
      "chatbot development",
      "dialogue systems",
      "Natural Language Processing",
      "text mining",
      "Search systems",
      "Recommendation systems",
      "Prompt engineering",
      "LLM fine-tuning",
      "model optimization",
      "AI agent architectures",
      "orchestration",
      "Model Context Protocol (MCP)",
      "Python",
      "scikit-learn",
      "spacy",
      "nltk",
      "pytorch",
      "tensorflow",
      "huggingface",
      "LangChain",
      "LlamaIndex",
      "SQL",
      "Oracle",
      "MongoDB",
      "graph database",
      "Pinecone",
      "Weaviate",
      "spark",
      "Linux",
      "shell scripting",
      "AWS",
      "Azure ML"
    ]
  }
}
```
**Node 2 Verdict:** 
```xml
<thinking>
Anchors identified:
- Company: Gartner
- University: Fairfield University

Primary high-frequency titles aligned with role:
- Data Scientist
- Machine Learning Engineer
- AI Engineer

Broader higher-frequency variations:
- Senior Data Scientist
- Data Science Manager
- Machine Learning Specialist

States structured deterministically per instructions.
</thinking>

<verdict>

STATE 1
Anchors:
- Company: Gartner
- University: Fairfield University

Titles:
- Data Scientist
- Machine Learning Engineer
- AI Engineer


STATE 2
Anchors:
- Company: Gartner
- University: Fairfield University

Titles:
- Senior Data Scientist
- Data Science Manager
- Machine Learning Specialist


STATE 3
Anchors:
- Company: Gartner

Titles:
- Senior Data Scientist
- Data Science Manager
- Machine Learning Specialist

</verdict>
```


**Final Output:**
```
Gartner Fairfield University ("Data Scientist" OR "Machine Learning Engineer" OR "AI Engineer")
```


#### Step D
**Input:**

```
5 PDFs of query returned profiles
```

**Node 1 Output:**
 ```
{
  "leads": [
    {
      "name": "Dylan Meyer",
      "company": "Gartner",
      "role": "Director, Data Science",
      "skills": [
        "Generative AI",
        "Natural Language Processing (NLP)",
        "Strategic Roadmaps"
      ],
      "university": "Fairfield University"
    },
    {
      "name": "Thi Hong Thinh DOAN",
      "company": "Self Employed",
      "role": "Economic consultant",
      "skills": [
        "Creative Writing",
        "Research Skills",
        "Economic Research"
      ],
      "university": "Aix-Marseille University"
    },
    {
      "name": "Aaron Tobias",
      "company": "SWBC",
      "role": "Principal Software Engineer, Security",
      "skills": [
        "Requirements Gathering",
        "User Provisioning",
        "Security Assertion Markup Language (SAML)"
      ],
      "university": "Rensselaer Polytechnic Institute"
    },
    {
      "name": "Adam Ware",
      "company": "Analytic-Aware LLC",
      "role": "Consultant & Founder - Data Strategy & Viz Leader, Analytics Advisor, Insights Expert",
      "skills": [
        "Design Thinking",
        "Quantitative Analytics",
        "Cross-functional Team Leadership"
      ],
      "university": "Cornell University"
    },
    {
      "name": "Jessica Hawthorne-Castro",
      "company": "Hawthorne Advertising",
      "role": "Chief Executive Officer",
      "skills": [
        "Media Buying",
        "Direct Response",
        "Integrated Marketing"
      ],
      "university": "Loyola Marymount University"
    }
  ]
}
```

**Node 2 Verdict:** 
```xml
<thinking>
Received 5 independent leads.
For each lead:
- Define tone (one of allowed values).
- Provide concise outreach angle.
- Include explicit call to action (e.g., 15-min chat, quick call, brief conversation).
- No ranking or relevance commentary.
</thinking>

<verdict>

<lead>
  <name>Dylan Meyer</name>
  <tone>professional_peer</tone>
  <strategy>
    Reference his leadership in Data Science and Generative AI initiatives at Gartner.
    Position outreach around shared interest in AI applications and data science impact.
    Call to action: Ask for a 15-minute conversation to learn about his journey to Director level and advice on growing within data science leadership.
  </strategy>
</lead>

<lead>
  <name>Thi Hong Thinh DOAN</name>
  <tone>curious_explorer</tone>
  <strategy>
    Highlight her background in economics, modeling, and data science across academia and consulting.
    Express curiosity about transitioning between research and applied quantitative roles.
    Call to action: Request a short virtual coffee chat to understand how she navigates academic and consulting work.
  </strategy>
</lead>

<lead>
  <name>Aaron Tobias</name>
  <tone>professional_peer</tone>
  <strategy>
    Acknowledge his work in security engineering, decentralized identity, and AI/LLM integration.
    Connect around technical innovation and applied AI systems.
    Call to action: Invite him to a brief 20-minute discussion to exchange perspectives on AI and secure system architecture.
  </strategy>
</lead>

<lead>
  <name>Adam Ware</name>
  <tone>warm_alumni</tone>
  <strategy>
    Reference shared academic affiliation and his experience spanning Gartner, consulting, and analytics leadership.
    Emphasize interest in analytics transformation and executive data storytelling.
    Call to action: Ask for a 15-minute alumni conversation to hear about his transition into advisory and consulting leadership.
  </strategy>
</lead>

<lead>
  <name>Jessica Hawthorne-Castro</name>
  <tone>curious_explorer</tone>
  <strategy>
    Recognize her leadership in performance-driven marketing and data-informed strategy.
    Express interest in how analytics and executive leadership intersect in agency environments.
    Call to action: Request a short introductory call to learn how she integrates data science into marketing strategy at scale.
  </strategy>
</lead>

</verdict>
```


> **Final Output:**
```
Hi Dylan,

I came across your work as Director of Data Science at Gartner and was particularly interested in your focus on Generative AI and NLP. It’s impressive to see how you’ve evolved within the organization into a leadership role in data science. I’m currently exploring how to grow toward more senior data science leadership positions and would really value your perspective.

Would you be open to a 15-minute conversation to share a bit about your journey and any advice you might have?

---

Hi Thi Hong Thinh,

Your background combining economics, research, and data science caught my attention—especially your work spanning consulting and academic research. I’m fascinated by professionals who bridge rigorous economic modeling with applied analytics.

If you’re open to it, I’d love to schedule a short virtual coffee chat to learn more about how you’ve navigated between research and consulting roles and what you’ve found most impactful along the way.

---

Hi Aaron,

I was really interested in your work in security engineering and your involvement with decentralized identity and AI/LLM-focused innovation. It’s exciting to see how these areas are converging in practice.

If you’re open to it, I’d appreciate a brief 20-minute conversation to exchange perspectives on building secure systems while integrating emerging AI capabilities.

---

Hi Adam,

I noticed your background spanning analytics leadership, consulting, and work with Gartner, along with your strong focus on data visualization and quantitative analytics. It’s inspiring to see how you’ve built a career around translating complex data into strategic insight.

As a fellow academic alum, I’d really value the chance to connect. Would you be open to a 15-minute conversation to share how you transitioned into advisory and analytics leadership?

---

Hi Jessica,

I’ve been following your leadership at Hawthorne Advertising and was struck by how strongly you emphasize blending storytelling with advanced data science to drive measurable performance. That integration of analytics and executive strategy is something I’m very interested in.

If you’re available, I’d love to schedule a short introductory call to learn more about how you incorporate data-driven thinking into marketing strategy at scale.


---


```

#### 2.5 Value Definition (The KPI Dashboard)
```
| Metric                      | Current (Manual)             | Target (AI)                               | Estimated Impact                                                |
| --------------------------- | ---------------------------- | ----------------------------------------- | --------------------------------------------------------------- |
| Outreach Volume (Frequency) | 8–12 leads/week              | 8–12 leads/week (same or higher possible) | Maintains output with less effort; potential to increase volume |
| Time per Profile Review     | 3–5 min                      | 1–2 min                                   | ~60% reduction                                                  |
| Time per Message Draft      | 7–10 min                     | 2–4 min                                   | ~60–70% reduction                                               |
| Total Weekly Time           | 2–3 hrs/week                 | 1–1.5 hrs/week                            | 1–1.5 hrs saved/week (50–70% reduction)                         |
| Cognitive Load              | High                         | Moderate/Low                              | Reduced fatigue → higher consistency & quality                  |
| Process Scalability         | Linear (time grows per lead) | Semi-automated                            | Enables 2× throughput with same time                            |

```

**Notes on benchmarks used (where PDD data was absent):**
Job criteria extraction: Industry benchmark for manual job posting parsing is 3–5 min; LLM-based extraction typically runs under 60 seconds.
Connection prioritization: Manual LinkedIn filtering estimated at 5–7 min per search session based on standard UX research on professional search workflows; AI ranking reduces this to a review-only task.

### ChatGPT/Claude logs
https://chatgpt.com/share/69a24e05-12c0-8007-bde4-d6af6968991f
