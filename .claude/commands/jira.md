---
description: Load current cycle stories and epic to Jira with proper parent links
---

You are being asked to load an epic and its user stories from a product discovery cycle into Jira.

# Task

1. **Record start time**:
   - Capture the current timestamp as the operation start time
   - This will be used for timing metrics

2. **Identify the cycle**:
   - Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
   - If not specified, look in `product/requirements/` for the most recent cycle (by date prefix)
   - Ask the user to clarify if there are multiple recent cycles

3. **Verify requirements exist**:
   - Check that `product/requirements/{cycle-name}/` directory exists
   - Find the epic file (epic-{number}-{slug}.md)
   - Find all story files (story-{number}-{slug}.md)
   - If no requirements found, inform the user they need to run `/req` first

4. **Get Jira project information**:
   - Use the mcp__atlassian__getAccessibleAtlassianResources tool to get the cloud ID
   - Use the mcp__atlassian__getVisibleJiraProjects tool to find the correct project
   - The project key should be "SCRUM" (NAM Demo project)

5. **Create the epic in Jira**:
   - Read the epic markdown file
   - Extract: title (from "# Epic:" line), description (user story section), labels, priority
   - Use mcp__atlassian__createJiraIssue to create the epic
   - Epic issue type name should be "Epic"
   - Note the created epic key (e.g., SCRUM-56)

6. **Create all stories in Jira**:
   - For each story file in the cycle:
     - Read the story markdown file
     - Extract: title (from "# User Story:" line), description (user story text), acceptance criteria, labels, priority, story points
     - Use mcp__atlassian__createJiraIssue to create the story
     - Issue type should be "Story"
     - Note the created story key (e.g., SCRUM-57, SCRUM-58, etc.)

7. **Link all stories to the epic**:
   - For each created story:
     - Use mcp__atlassian__editJiraIssue with `{"fields": {"parent": {"key": "SCRUM-XX"}}}`
     - This sets the epic as the parent of the story
   - Verify all stories are properly linked

8. **Record timing and report results**:
   - Capture the end timestamp
   - Calculate duration in seconds
   - Read or create timing.json in the cycle directory (use the discovery cycle path, not requirements)
   - Add this operation to the operations array:
     ```json
     {
       "command": "/jira",
       "start": "{start_timestamp_ISO8601}",
       "end": "{end_timestamp_ISO8601}",
       "duration_seconds": {duration},
       "status": "success",
       "metadata": {
         "epic_created": "SCRUM-XX",
         "stories_created": {count},
         "story_keys": ["SCRUM-XX", "SCRUM-YY", ...]
       }
     }
     ```
   - Update total_duration_seconds
   - Append to global timing log at `artifacts/timing-log.jsonl`:
     ```json
     {"timestamp": "{end_timestamp}", "command": "/jira", "cycle": "{cycle-name}", "duration_seconds": {duration}, "status": "success", "metadata": {"epic_created": "SCRUM-XX", "stories_created": {count}}}
     ```
   - Tell the user:
     - How many issues were created
     - The epic key and title
     - All story keys and titles
     - Confirm all stories are linked to the epic
     - The operation duration
     - Summary (e.g., "Created 1 epic and 8 stories in Jira in 10 minutes, all linked")

# Notes

- The epic must be created FIRST before the stories
- All stories must be linked to the epic using the parent field
- Use the exact project key "SCRUM" for NAM Demo
- Story descriptions should include the acceptance criteria section from the markdown
- Labels from the markdown should be applied to the Jira issues
- If any creation fails, report the error and continue with remaining stories
- The cloudId for NAM Demo should be obtained from getAccessibleAtlassianResources
