---
description: Extract user stories and requirements from discovery synthesis
---

You are being asked to extract user stories and requirements from a completed discovery cycle synthesis.

# Task

1. **Record start time**:
   - Capture the current timestamp as the operation start time
   - This will be used for timing metrics

2. **Identify the cycle**:
   - Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
   - If not specified, look in `product/discovery/` for the most recent cycle (by date prefix)
   - Ask the user to clarify if there are multiple recent cycles

3. **Verify synthesis exists**:
   - Check that `product/discovery/{cycle-name}/synthesis-{date}.md` exists
   - If no synthesis found, inform the user they need to run `/synth` first
   - Read the synthesis document to understand the features and requirements

4. **Determine story numbering**:
   - Read `product/requirements/stories-by-cycle.md` to find the highest existing story number
   - New stories should start at the next sequential number (e.g., if last is STORY-021, start at STORY-022)

5. **Run story extraction using Task agent**:
   - Use the Task tool with subagent_type="general-purpose"
   - Provide the agent with:
     - The synthesis document content
     - The story template from `product/templates/story-template.md`
     - The epic template from `product/templates/epic-template.md`
     - Context files from `product/context/` (product-overview.md, target-users.md, technical-context.md)
     - The next available story number to start from
   - Instruct the agent to:
     - Create an epic document first
     - Extract user stories following the template format
     - Use Given-When-Then acceptance criteria
     - Assign appropriate priorities (Must have, Should have, Could have)
     - Provide effort estimates
     - Identify dependencies between stories
     - Update stories-by-cycle.md with the new stories

6. **Save requirements output**:
   - Create directory `product/requirements/{cycle-name}/` if it doesn't exist
   - Save epic as `product/requirements/{cycle-name}/epic-{number}-{slug}.md`
   - Save each story as `product/requirements/{cycle-name}/story-{number}-{slug}.md`
   - Update `product/requirements/stories-by-cycle.md` with the new cycle section

7. **Record timing and report results**:
   - Capture the end timestamp
   - Calculate duration in seconds
   - Read or create timing.json in the cycle directory
   - Add this operation to the operations array:
     ```json
     {
       "command": "/req",
       "start": "{start_timestamp_ISO8601}",
       "end": "{end_timestamp_ISO8601}",
       "duration_seconds": {duration},
       "status": "success",
       "metadata": {
         "epic_created": "EPIC-XXX",
         "stories_created": {count}
       }
     }
     ```
   - Update total_duration_seconds
   - Append to global timing log at `artifacts/timing-log.jsonl`:
     ```json
     {"timestamp": "{end_timestamp}", "command": "/req", "cycle": "{cycle-name}", "duration_seconds": {duration}, "status": "success", "metadata": {"epic_created": "EPIC-XXX", "stories_created": {count}}}
     ```
   - Tell the user:
     - Story extraction is complete
     - List the epic and all stories created with their titles and priorities
     - Summary: X stories (Y must have, Z should have, etc.)
     - Estimated total effort
     - The operation duration
     - Note that stories are ready to be loaded to Jira with `/jira`

# Notes

- Stories should follow Given-When-Then format for acceptance criteria
- Each story should have: functional scenarios, non-functional requirements, quality checklist
- Epic should have: overview, business value, success metrics, story list
- DO NOT automatically load stories to Jira - that's a separate workflow
- The Task agent should synthesize from the synthesis, not just copy content
- Stories should be properly sized (S/M/L) and have effort estimates in days
