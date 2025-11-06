---
description: Load current cycle stories and epic to Jira with proper parent links
---

You are being asked to load an epic and its user stories from a product discovery cycle into Jira.

# Overview

This command orchestrates the Jira loading workflow by reading the canonical prompt instructions and executing them.

# Workflow Steps

## 1. Record Start Time
- Capture the current timestamp as the operation start time
- This will be used for timing metrics

## 2. Identify the Cycle
- Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
- If not specified, look in `product/requirements/` for the most recent cycle (by date prefix)
- Ask the user to clarify if there are multiple recent cycles

## 3. Verify Requirements Exist
- Check that `product/requirements/{cycle-name}/` directory exists
- Find the epic file (epic-{number}-{slug}.md)
- Find all story files (story-{number}-{slug}.md)
- If no requirements found, inform the user they need to run `/req` first

## 4. Read the Jira Loading Prompt
**Read and follow the instructions in**: `product/prompts/load-stories-to-tracker.md`

This prompt contains the canonical instructions for:
- How to get Jira project information
- How to extract data from epic and story markdown files
- How to map markdown fields to Jira fields
- How to create issues in the correct order
- How to link stories to epics
- How to handle errors and retries

## 5. Execute Jira Loading
Follow the instructions from the prompt to load the requirements to Jira.

**Key requirements:**
- Use Atlassian MCP tools for all Jira operations
- Create epic first, then stories
- Link all stories to the epic as parent
- Preserve all acceptance criteria and metadata
- Handle any Jira-specific field mappings

## 6. Record Timing and Report Results
- Capture the end timestamp
- Calculate duration in seconds
- Read or create `timing.json` in the cycle directory
- Add this operation to the operations array:
  ```json
  {
    "command": "/jira",
    "start": "{start_timestamp_ISO8601}",
    "end": "{end_timestamp_ISO8601}",
    "duration_seconds": {duration},
    "status": "success",
    "metadata": {
      "epic_created": "PROJ-XXX",
      "stories_created": ["PROJ-YYY", "PROJ-ZZZ"],
      "jira_project": "PROJ"
    }
  }
  ```
- Update total_duration_seconds
- Append to global timing log at `artifacts/timing-log.jsonl`:
  ```json
  {"timestamp": "{end_timestamp}", "command": "/jira", "cycle": "{cycle-name}", "duration_seconds": {duration}, "status": "success", "metadata": {"epic_created": "PROJ-XXX", "stories_count": {count}}}
  ```
- Tell the user:
  - Jira loading is complete
  - The epic key and link
  - List of all story keys and titles
  - Summary: X stories loaded to Jira project Y
  - Direct links to view the epic and stories in Jira
  - The operation duration

# Important Notes

- **The prompt file is the source of truth** for Jira loading logic
- Users can customize Jira loading behavior by editing `product/prompts/load-stories-to-tracker.md`
- This command handles workflow orchestration (finding files, timing, reporting)
- The prompt handles the actual Jira API interaction logic
- Requires Atlassian MCP to be configured with appropriate permissions
- If Atlassian MCP is not available, inform the user and skip gracefully
