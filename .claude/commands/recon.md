---
description: Reconcile release notes and update product spec
---

You are being asked to reconcile release notes from a build increment with stories and update the product specification.

# Overview

This command orchestrates the reconciliation workflow: processing release notes, updating story statuses, managing backlog, and updating the product specification.

# Workflow Steps

## 1. Record Start Time
- Capture the current timestamp as the operation start time
- This will be used for timing metrics

## 2. Identify the Iteration
- Check if the user specified an iteration name (e.g., "2025-11-12-mvp")
- If not specified, ask the user which iteration these release notes are for
- Look in `product/iterations/` to verify iteration exists

## 3. Get Release Notes
- Ask the user for release notes (file path, content, or URL)
- If file path provided, read the file
- If content provided directly, use it
- Release notes should ideally reference story IDs (STORY-XXX format)

## 4. Read the Reconciliation Prompt
**Read and follow the instructions in**: `product/prompts/reconcile-and-update-spec.md`

This prompt contains the canonical instructions for:
- How to parse release notes and extract story IDs
- How to match release notes to stories when IDs aren't explicit
- How to update story statuses (Ready → Built)
- How to identify stories that weren't built
- How to update backlog with unbuilt stories
- How to create release artifacts
- How to update the product specification

## 5. Execute Reconciliation
Follow the instructions from the prompt to reconcile the release.

**Key requirements:**
- Parse release notes for story IDs
- If story IDs not found, ask user to map stories to release notes
- Update story files: status Ready → Built, add build date
- Identify Ready stories not in release notes (candidates for backlog)
- Ask user about each unbuilt Ready story: move to backlog? (y/n/skip)
- Create release artifact in `product/iterations/{iteration}/releases/`
- Update `product/product-spec.md` with newly built capabilities
- Update `product/backlog.md` if stories moved to backlog

## 6. Record Timing and Report Results
- Capture the end timestamp
- Calculate duration in seconds
- Read or create `timing.json` in the iteration directory
- Add this operation to the operations array:
  ```json
  {
    "command": "/recon",
    "start": "{start_timestamp_ISO8601}",
    "end": "{end_timestamp_ISO8601}",
    "duration_seconds": {duration},
    "status": "success",
    "metadata": {
      "stories_built": {count},
      "stories_to_backlog": {count},
      "release_number": {number}
    }
  }
  ```
- Update total_duration_seconds
- Append to global timing log at `product/artifacts/timing-log.jsonl`:
  ```json
  {"timestamp": "{end_timestamp}", "command": "/recon", "iteration": "{iteration-name}", "duration_seconds": {duration}, "status": "success", "metadata": {"stories_built": {count}, "stories_to_backlog": {count}}}
  ```
- Tell the user:
  - Reconciliation is complete
  - X stories marked as Built
  - Y stories moved to backlog
  - Product spec updated with new capabilities
  - Path to release artifact
  - The operation duration

# Important Notes

- **The prompt file is the source of truth** for reconciliation logic
- Users can customize reconciliation behavior by editing `product/prompts/reconcile-and-update-spec.md`
- This command handles workflow orchestration (getting input, timing, reporting)
- The prompt handles the actual reconciliation logic
- Stories without "Building" status - they go directly from Ready to Built
- Reconciliation is atomic: release notes → story updates → backlog → product spec
- Release artifacts provide historical record of what was built when
