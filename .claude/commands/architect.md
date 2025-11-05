Architecture and planning workflow for tickets in "Idea" phase.

The architect-ticket workflow will:
1. Fetch tickets in Idea phase (Backlog, To Do)
2. Let you select a ticket to architect
3. Read the current architecture spec for context
4. Analyze requirements and constraints
5. Design the solution with Mermaid diagrams
6. Generate comprehensive solution document
7. Break down into 3-8 implementable subtasks
8. Create subtasks in Jira automatically

Execute:
```bash
npm run architect-ticket
```

The solution will be saved to:
```
.ai-context/solutions/<TICKET-ID>_<slug>/solution.md
.ai-context/solutions/<TICKET-ID>_<slug>/architecture-diagram.md
.ai-context/solutions/<TICKET-ID>_<slug>/metadata.json
```

Subtasks will be created in Jira linked to the parent ticket.

Review the solution and subtasks, then move the ticket to "Ready for Development" when approved.
