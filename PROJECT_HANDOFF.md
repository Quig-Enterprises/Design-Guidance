### **Prompt for the Old/Current Manus AI Session:**

Your current session is concluding. You must now perform a formal project handoff to a new Manus AI session to ensure seamless continuity.

Your task is to generate a single, self-contained briefing document that will be given to the new session. This document must contain all necessary context, project history, and explicit instructions for the new session to pick up the work exactly where we left off.

**The briefing document you generate must include the following sections:**

1.  **Project Mission:** State that the new session's mission is to continue developing the comprehensive design and development guidance for CxQ (Creations by Q), the development identity for Quig Enterprises, LLC.

2.  **Project History & Status:**
    *   Summarize the work completed so far: the creation of a suite of Markdown guidance documents.
    *   List all created documents by filename (`README.md`, `DESIGN_STRATEGY.md`, `NAMING_CONVENTIONS.md`, `WORDPRESS_OUTPUT_STRUCTURE.md`, `REVISIONING.md`, `STANDALONE_LIBRARIES.md`, `AVAILABLE_LIBRARIES.md`).
    *   Detail the contents of the `AVAILABLE_LIBRARIES.md` catalog, listing the four libraries (Data Logger, Credential Manager, Notification Engine, Workflow Engine).
    *   Crucially, include the note that these four libraries are currently developed and maintained within the main "CxQ Membership Plugin" and are not yet standalone.

3.  **Instructions for the New Session:** This is important. Create a clear, actionable task list for the new session. It must instruct the new session to:
    *   **Task 1: Ingest and Verify Current Guidance.** Instruct it to perform a `git pull` from the `https://github.com/Quig-Enterprises/Design-Guidance` repository to get the latest documents.
    *   **Task 2: Identify Opportunities for Improvement and Compliance.** Instruct it to analyze the guidance documents and identify areas for improvement. Provide these specific sub-tasks:
        *   **Analyze `AVAILABLE_LIBRARIES.md`:** Suggest improving the note about the libraries' embedded status. Propose adding a "Status" field (e.g., `Standalone`, `Embedded`, `In Development`) to the catalog entry for each library.
        *   **Cross-Reference all Documents:** Instruct it to check for any inconsistencies or contradictions between the documents.
        *   **Propose a "Guidance Version":** Instruct it to propose adding a version number to the main `README.md` and suggest a process for updating it, following the rules in `REVISIONING.md`.

4.  **Required Deliverable:** Specify that the new session's first output should be a report summarizing its findings, including a confirmation of the `git pull` and a list of actionable suggestions for improvement, referencing the specific documents.

Generate this entire briefing as a single, downloadable document formatted in Markdown, ready to be used as the initial prompt for the new chat session.