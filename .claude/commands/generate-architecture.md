Generate complete architecture specification from your Jira project.

This command will:
1. Fetch ALL tickets from your Jira project
2. Analyze requirements and identify patterns
3. Generate a comprehensive Project Brief
4. Generate an Architecture Specification with:
   - Technology stack recommendations (with justification)
   - System architecture design
   - Data models and API design
   - Architecture Decision Records (ADRs)
   - Development phases
   - Risk analysis

The AI will recommend technologies based on the requirements it finds in your tickets, and you can review and customize the recommendations.

Execute:
```bash
npm run generate-architecture
```

You'll be prompted to add additional context (business goals, constraints, etc.) before generation.

Outputs:
- `.ai-context/project-brief.md` - High-level project overview
- `.ai-context/architecture-spec.md` - Comprehensive architecture design
- `.ai-context/founding-spec.md` - Alias for architecture spec

After generation, review the specs and then start working on tickets with:
```bash
npm run fetch-tickets
```
