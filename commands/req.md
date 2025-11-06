---
description: Extract user stories and requirements from discovery synthesis
---

You are being asked to extract user stories and requirements from a completed discovery cycle synthesis.

# Overview

This command orchestrates the requirements extraction workflow by reading the canonical prompt instructions and executing them.

# Workflow Steps

## 1. Record Start Time
- Capture the current timestamp as the operation start time
- This will be used for timing metrics

## 2. Identify the Cycle
- Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
- If not specified, look in `product/discovery/` for the most recent cycle (by date prefix)
- Ask the user to clarify if there are multiple recent cycles

## 3. Verify Synthesis Exists
- Check that `product/discovery/{cycle-name}/synthesis-{date}.md` exists
- If no synthesis found, inform the user they need to run `/synth` first
- Read the synthesis document to understand the features and requirements

## 4. Determine Story Numbering
- Read `product/requirements/stories-by-cycle.md` to find the highest existing story number
- New stories should start at the next sequential number (e.g., if last is STORY-021, start at STORY-022)

## 5. Read the Story Extraction Prompts
**Read and follow the instructions in**:
- `product/prompts/extract-user-stories.md` - For extracting stories from synthesis
- `product/prompts/generate-acceptance-criteria.md` - For writing acceptance criteria

These prompts contain the canonical instructions for:
- How to convert synthesis findings into user stories
- How to structure epics
- How to write Given-When-Then acceptance criteria
- How to assign priorities and estimates
- How to identify dependencies
- What quality checks to include

## 6. Execute Story Extraction
Follow the instructions from the prompts to create the requirements documents.

**Key requirements:**
- Use the epic template from `product/requirements/epic-template.md`
- Use the story template from `product/requirements/story-template.md`
- Include product context from `product/context/`
- Ensure sequential story numbering
- Follow Given-When-Then format for acceptance criteria

## 7. Save Requirements Output
- Create directory `product/requirements/{cycle-name}/` if it doesn't exist
- Save epic as `product/requirements/{cycle-name}/epic-{number}-{slug}.md`
- Save each story as `product/requirements/{cycle-name}/story-{number}-{slug}.md`
- Update `product/requirements/stories-by-cycle.md` with the new cycle section

## 8. Record Timing and Report Results
- Capture the end timestamp
- Calculate duration in seconds
- Read or create `timing.json` in the cycle directory
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

# Important Notes

- **The prompt files are the source of truth** for extraction and acceptance criteria logic
- Users can customize story extraction by editing the prompt files in `product/prompts/`
- This command handles workflow orchestration (finding files, numbering, timing, saving output)
- The prompts handle the actual extraction logic and requirements
- DO NOT automatically load stories to Jira - that's a separate workflow (`/jira`)
