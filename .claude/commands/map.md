---
description: Create Miro story map for current cycle with production-grade formatting
---

You are being asked to create a visual story map in Miro from a product discovery cycle's requirements.

# Overview

This command orchestrates the story mapping workflow by reading the canonical prompt instructions and executing them to create a production-grade Miro board.

# Workflow Steps

## 1. Record Start Time
- Capture the current timestamp as the operation start time
- This will be used for timing metrics

## 2. Identify the Cycle
- Check if the user specified a cycle name (e.g., "2025-11-12-mvp")
- If not specified, look in `product/requirements/` for the most recent cycle (by date prefix)
- Ask the user to clarify if there are multiple recent cycles

## 3. Verify Requirements Exist
- Check that `product/requirements/{cycle-name}/` directory exists
- Find the epic file (epic-{number}-{slug}.md)
- Find all story files (story-{number}-{slug}.md)
- Find STORIES-SUMMARY.md for release prioritization
- If no requirements found, inform the user they need to run `/req` first

## 4. Create Story Map Directory
- Create directory: `product/story-maps/{cycle-name}/`
- This is where the story map markdown and metadata will be stored

## 5. Read the Story Mapping Prompt
**Read and follow the instructions in**: `product/prompts/create-story-map.md`

This prompt contains the canonical instructions for:
- How to analyze epic and stories to extract activities
- How to create a Miro board
- How to apply the universal color scheme by story type
- How to position items with consistent spacing
- How to create swim lanes with connector-based separators
- How to add persona emojis and legend
- How to save metadata for future syncing

## 6. Execute Story Map Creation
Follow the instructions from the prompt to create the Miro story map.

**Key requirements:**
- Use Miro MCP tools for all board operations
- Apply production-grade formatting (blue activity headers, color by type, consistent spacing)
- Create connector-based swim lanes (NOW/NEXT/LATER)
- Include persona emojis on all story cards
- Save comprehensive metadata to miro-metadata.json
- Create human-readable story-map.md documentation

## 7. Record Timing and Report Results
- Capture the end timestamp
- Calculate duration in seconds
- Read or create `timing.json` in the cycle discovery directory (`product/discovery/{cycle-name}/timing.json`)
- Add this operation to the operations array:
  ```json
  {
    "command": "/map",
    "start": "{start_timestamp_ISO8601}",
    "end": "{end_timestamp_ISO8601}",
    "duration_seconds": {duration},
    "status": "success",
    "metadata": {
      "board_id": "uXjVJpSkPjY=",
      "board_url": "https://miro.com/app/board/uXjVJpSkPjY=",
      "total_items_created": 37,
      "story_cards": 18
    }
  }
  ```
- Update total_duration_seconds
- Append to global timing log at `artifacts/timing-log.jsonl`:
  ```json
  {"timestamp": "{end_timestamp}", "command": "/map", "cycle": "{cycle-name}", "duration_seconds": {duration}, "status": "success", "metadata": {"board_id": "xxx", "story_count": {count}}}
  ```
- Tell the user:
  - Story map creation is complete
  - Direct link to the Miro board
  - Summary: X stories mapped across Y activities
  - Path to story-map.md documentation
  - The operation duration

# Important Notes

- **The prompt file is the source of truth** for story mapping logic
- Users can customize story map formatting by editing `product/prompts/create-story-map.md`
- This command handles workflow orchestration (finding files, timing, reporting)
- The prompt handles the actual Miro API interaction and formatting logic
- Requires Miro MCP to be configured with appropriate permissions
- If Miro MCP is not available, inform the user and skip gracefully
- Story maps are synced to markdown for version control
