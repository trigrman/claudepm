---
description: Run synthesis on the current discovery cycle
---

You are being asked to synthesize the discovery materials for the current or specified product discovery cycle.

# Overview

This command orchestrates the synthesis workflow by reading the canonical prompt instructions and executing them.

# Workflow Steps

## 1. Record Start Time
- Capture the current timestamp as the operation start time
- This will be used for timing metrics

## 2. Identify the Cycle
- Check if the user specified a cycle name (e.g., "2025-10-30-dark-mode")
- If not specified, look in `product/discovery/` for the most recent cycle (by date prefix)
- Ask the user to clarify if there are multiple recent cycles

## 3. Read the Synthesis Prompt
**Read and follow the instructions in**: `product/prompts/synthesize-discovery.md`

This prompt contains the canonical instructions for:
- What context files to review
- How to identify themes and patterns
- How to extract user needs
- How to rank pain points
- How to propose features
- How to structure the output

## 4. Execute Synthesis
Follow the instructions from the prompt to create the synthesis document.

**Key requirements:**
- Use the synthesis template from `product/discovery/synthesis-template.md`
- Review all discovery materials in the cycle directory
- Include product context from `product/context/`
- Cross-reference with previous cycles
- Provide evidence-based recommendations

## 5. Save Output
- Save to: `product/discovery/{cycle-name}/synthesis-{date}.md`
- Use ISO date format (YYYY-MM-DD) for the filename
- Remove the `.synthesis-pending` marker file if it exists

## 6. Record Timing and Report Results
- Capture the end timestamp
- Calculate duration in seconds
- Read or create `timing.json` in the cycle directory
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

# Important Notes

- **The prompt file is the source of truth** for synthesis instructions
- Users can customize synthesis behavior by editing `product/prompts/synthesize-discovery.md`
- This command handles workflow orchestration (finding files, timing, saving output)
- The prompt handles the actual synthesis logic and requirements
