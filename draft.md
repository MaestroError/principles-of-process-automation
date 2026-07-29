The Five O Principles of Process Automation
-------------------------------------------

The "Five O" is a universal modeling language for process automation. It bridges the gap between intent, execution, and evolution. Whether you are writing a prompt, designing an AI agent orchestrator, or coding traditional software, a process is only robust if it defines these five dimensions.

### 1. Objective (What is the goal and its boundaries?)
The Objective is the complete "Definition of Done." It unites the strategic purpose of the process with the strict, non-negotiable deliverables required for success.
-   **The Rule:** It must define both the context (the audience, the format, the "why") and the strict constraints (the absolute Dos and Don'ts).
-   **Example:** *"Write a post to get project managers interested in Jira automation (Context), using the provided data and simple words, without ever adding hashtags (Constraints)."*

### 2. Occurrence (When does it start?)
The Occurrence is the unity of circumstances that must be met for the automation to ignite. It encompasses both the trigger event and the prerequisites.
-   **The Rule:** A process should never run blindly; it executes only when the exact required conditions, data, and permissions are present in the environment.
-   **Example:** *"Run when an email is received, marked as important, from a specific domain list, and contains a PDF attachment."*

### 3. Order (In what sequence?)
The Order defines the dependency tree of the process. It establishes what must logically happen before something else is allowed to happen.
-   **The Rule:** Rather than micromanaging every single micro-step, it maps the critical dependencies and milestones to guarantee the integrity of the workflow.
-   **Example:** *"Plan the implementation first, draft the PR second, review it third, and merge only after the review is approved."*

### 4. Option (What if the primary path isn't possible?)
The Option mandates that alternative paths and fallback states are designed from the beginning. It acknowledges that automations exist in fragile environments dependent on external variables.
-   **The Rule:** A process must define how to gracefully degrade, pivot, or escalate when roadblocks occur. The more options covered, the more resilient the automation.
-   **Example:** Ranging from alternative execution paths (*"If the API fails, scrape the site"*) to safe failure states (*"If the goal cannot be achieved, move the task to a manual review queue"*).

### 5. Observation (How do we measure and improve?)
Observation is the mandatory requirement for visibility. It defines how the system tracks execution, determines long-term success, and creates a feedback loop.
-   **The Rule:** An automation cannot be a black box. It must produce the telemetry and insights necessary to evaluate the paths taken, measure success, and continuously evolve the process itself.
-   **Example:** *"Log the time taken, the tools used, and the fallback paths triggered, so we can periodically refine the prompt or update the dependency tree based on where the system struggles."*

The 5Os principles cover the Setup (Objective, Occurrence), the Execution (Order, Option), and the Evolution (Observation).