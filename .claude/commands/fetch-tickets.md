Fetch open tickets from your configured ticket system (Jira or GitHub Issues).

This command will:
1. Connect to your ticket system
2. Fetch open/ready tickets
3. Display a list for selection
4. Optionally architect a selected ticket

Execute:
```bash
npm run fetch-tickets
```

Options:
- Limit number of results: `npm run fetch-tickets -- --limit 20`

The command will show ticket IDs, titles, and statuses, then prompt you to select one for architecture.
