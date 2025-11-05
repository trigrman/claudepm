---
description: Run synthesis on the current discovery cycle
---

You are being asked to synthesize the discovery materials for the current or specified product discovery cycle.

# Task

1. **Record start time**:
   - Capture the current timestamp as the operation start time
   - This will be used for timing metrics

2. **Identify the cycle**:
   - Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
   - If not specified, look in `product/discovery/` for the most recent cycle (by date prefix)
   - Ask the user to clarify if there are multiple recent cycles

3. **Locate discovery materials**:
   - Read `product/discovery/{cycle-name}/README.md` for context
   - Read all files in `product/discovery/{cycle-name}/interviews/` (excluding template files)
   - Read all files in `product/discovery/{cycle-name}/observations/` (excluding template files)

4. **Run synthesis using Task agent**:
   - Use the Task tool with subagent_type="general-purpose"
   - Provide the agent with:
     - All discovery materials content
     - The synthesis template from `product/templates/synthesis-template.md`
     - Context files from `product/context/` (product-overview.md, target-users.md, etc.)
   - Instruct the agent to create a comprehensive synthesis document following the template

5. **Save synthesis output**:
   - Save to `product/discovery/{cycle-name}/synthesis-{date}.md`
   - Use ISO date format (YYYY-MM-DD) for the filename
   - Remove the `.synthesis-pending` marker file if it exists

6. **Record timing and report results**:
   - Capture the end timestamp
   - Calculate duration in seconds
   - Read or create timing.json in the cycle directory
   - Add this operation to the operations array:
     ```json
     {
       "command": "/synth",
       "start": "{start_timestamp_ISO8601}",
       "end": "{end_timestamp_ISO8601}",
       "duration_seconds": {duration},
       "status": "success"
     }
     ```
   - Update total_duration_seconds
   - Append to global timing log at `artifacts/timing-log.jsonl`:
     ```json
     {"timestamp": "{end_timestamp}", "command": "/synth", "cycle": "{cycle-name}", "duration_seconds": {duration}, "status": "success"}
     ```
   - Tell the user:
     - The synthesis is complete
     - The file path
     - Key findings summary (themes, features, effort estimate)
     - The operation duration

# Notes

- The synthesis should follow the template structure exactly
- Include all insights from interviews and observations
- Identify themes, features, technical recommendations, and open questions
- Provide effort estimates and risk assessment
- The Task agent should have autonomy to analyze and synthesize, not just copy content
