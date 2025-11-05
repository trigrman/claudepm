Initialize the AI development pipeline for this project.

This command will:
1. Detect the project type (Next.js, Express, etc.)
2. Set up configuration files
3. Create the .ai-context directory structure
4. Generate template documents (project brief, founding spec, constraints)

Execute the initialization wizard:
```bash
npm run init-project
```

Follow the prompts to configure:
- Project name
- Ticket source (Jira or GitHub)
- LLM provider and model
- Integration credentials

After initialization, remember to:
1. Update `.ai-context/project-brief.md` with your project details
2. Set up environment variables in `.env`
3. Review and customize `.ai-context/agents.yaml` if needed
