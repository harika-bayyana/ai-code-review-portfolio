# Code Review Methodology

This document outlines the systematic approach I use to evaluate AI-generated code. My goal is to produce **Specific, Actionable, and Reproducible** feedback that serves as a high-quality learning signal for model improvement.

## 1. The 3-Pass Review Approach

I avoid diving straight into line-by-line review. Instead, I follow three distinct phases:

### Phase 1: Map (Architecture & Strategy)
- **Objective**: Understand what the code is *trying* to do.
- - **Actions**: Identify the core algorithm, dependencies, and entry points. Match the implementation strategy against the prompt requirements.
  - - **Goal**: Detect high-level "strategy hallucinations" or missing functional requirements.
   
    - ### Phase 2: Trace (Logic & Execution)# Code Review Methodology
    -
    - This document outlines the systematic approach I use to evaluate AI-generated code. My goal is to produce **Specific, Actionable, and Reproducible** feedback that serves as a high-quality learning signal for model improvement.
    -
    - ## 1. The 3-Pass Review Approach
    -
    - I avoid diving straight into line-by-line review. Instead, I follow three distinct phases:
    -
    - ### Phase 1: Map (Architecture & Strategy)
    - - **Objective**: Understand what the code is *trying* to do.
      - - **Actions**: Identify the core algorithm, dependencies, and entry points. Match the implementation strategy against the prompt requirements.
        - - **Goal**: Detect high-level "strategy hallucinations" or missing functional requirements.
          -
          - ### Phase 2: Trace (Logic & Execution)
          - - **Objective**: Identify "silent" logical errors.
            - - **Actions**: Mentions dry-run tracing of variables. Check boundary conditions (empty lists, null inputs, extreme values). Look for common pitfalls like off-by-one errors or incorrect short-circuiting.
              - - **Goal**: Ensure the code actually works as intended across all edge cases.
                -
                - ### Phase 3: Explain (Reporting)
                - - **Objective**: Communicate findings professionally.
                  - - **Actions**: Structure feedback using the CEIA format. Cite specific line numbers and provide reproducible test cases.
                    - - **Goal**: Make the feedback immediately useful for model trainers and developers.
                      -
                      - ---
                      -
                      - ## 2. Priority of Evaluation
                      -
                      - When ranking model responses, I apply a strict prioritization hierarchy:
                      -
                      - 1.  **Functional Correctness**: Does the code solve the problem? Does it handle edge cases? (Broken code is a 1/5).
                        2.  2.  **Security**: Are there vulnerabilities (SQLi, XSS, ReDoS)? (Insecure code is a major penalty).
                            3.  3.  **Data & Schema Integrity**: For JSON/Data tasks, does it follow the required schema? Are types and structures strictly enforced?
                                4.  4.  **Code Quality & Style**: Does it follow language-specific idioms (PEP 8, Airbnb, Google Style)? Is it readable?
                                    5.  5.  **Performance**: Is the time and space complexity optimal for the task?
                                        6.
                                        7.  ---
                                        8.
                                        9.  ## 3. Justification Standard: CEIA
                                        10.
                                        11.  Every justification I write follows the **Claim -> Evidence -> Implication -> Actionable** format:
                                        12.
                                        13.  | Component | Purpose | Example |
                                        14.  |:---|:---|:---|
                                        15.  | **Claim** | State the core finding or preference. | "Response A is preferred due to robust input validation." |
                                        16.  | **Evidence** | Cite specific code or behavior. | "Line 12: `if (arr == null)` handles the null case which B misses." |
                                        17.  | **Implication** | Explain why this matters for the user/model. | "Without this check, the application would crash with a NullPointerException." |
                                        18.  | **Actionable** | Provide a concrete fix for the issue. | "Response B should add a null check before accessing `arr.length`." |
                                        19.
                                        20.  ---
                                        21.
                                        22.  ## 4. RLHF Studio Workflow
                                        23.
                                        24.  My evaluation process within the **RLHF Studio** platform involves:
                                        25.  - **Dimension Scoring**: Calibrating scores across multiple dimensions (Style, Correctness, Scalability).
                                             - - **Preference Scaling**: Using a 7-point scale to indicate the magnitude of preference (e.g., "A is much better than B" vs "A is slightly better").
                                               - - **Consistency Checks**: Ensuring that my justifications align perfectly with the scores assigned.
                                                 -     - - **Objective**: Identify "silent" logical errors.
      - - **Actions**: Mentions dry-run tracing of variables. Check boundary conditions (empty lists, null inputs, extreme values). Look for common pitfalls like off-by-one errors or incorrect short-circuiting.
        - - **Goal**: Ensure the code actually works as intended across all edge cases.
         
          - ### Phase 3: Explain (Reporting)
          - - **Objective**: Communicate findings professionally.
            - - **Actions**: Structure feedback using the CEIA format. Cite specific line numbers and provide reproducible test cases.
              - - **Goal**: Make the feedback immediately useful for model trainers and developers.
               
                - ---

                ## 2. Priority of Evaluation

                When ranking model responses, I apply a strict prioritization hierarchy:

                1.  **Functional Correctness**: Does the code solve the problem? Does it handle edge cases? (Broken code is a 1/5).
                2.  2.  **Security**: Are there vulnerabilities (SQLi, XSS, ReDoS)? (Insecure code is a major penalty).
                    3.  3.  **Data & Schema Integrity**: For JSON/Data tasks, does it follow the required schema? Are types and structures strictly enforced?
                        4.  4.  **Code Quality & Style**: Does it follow language-specific idioms (PEP 8, Airbnb, Google Style)? Is it readable?
                            5.  5.  **Performance**: Is the time and space complexity optimal for the task?
                              
                                6.  ---
                              
                                7.  ## 3. Justification Standard: CEIA
                              
                                8.  Every justification I write follows the **Claim 
