# Reconcile Release Notes and Update Product Specification

This prompt provides canonical instructions for reconciling release notes with stories and updating the product specification.

## Required Input
- **Iteration**: Which iteration these release notes are for
- **Release Notes**: Markdown file, text content, or structured data from build process

## Process Steps

### 1. Parse Release Notes

**Extract Story IDs:**
- Look for story ID patterns: `STORY-###`, `#STORY-###`, or similar
- Build list of story IDs mentioned in release notes

**If no story IDs found:**
- Ask user: "Release notes don't contain story IDs. Which stories were built in this release?"
- Present list of Ready stories from iteration for user to select
- Record mapping between release notes and stories

### 2. Update Story Statuses

For each story ID in release notes:

**Read story file** from `product/iterations/{iteration}/stories/story-{number}-*.md`

**Update story:**
- Change status: `Ready` → `Built`
- Add metadata field: `Build Date: {YYYY-MM-DD}`
- Save updated story file

**Example:**
```markdown
**Status**: Built
**Build Date**: 2025-11-20
```

### 3. Identify Unbuilt Stories

**Scan iteration stories:**
- List all stories with status `Ready` in `product/iterations/{iteration}/stories/`
- Exclude stories that are now `Built`
- These are candidates for backlog

**For each unbuilt Ready story:**
- Show user: Story ID, title, priority
- Ask: "Move STORY-XXX to backlog? (y/n/skip)"
- If yes: Add to backlog list with reason
- If no: Leave in iteration (may be work in progress)
- If skip: User will handle manually

### 4. Update Backlog

**Read** `product/backlog.md`

**For each story moved to backlog:**
- Add entry under appropriate priority section
- Format: `- **STORY-XXX: {title}** ({iteration-name})`
- Include reason in backlog notes if provided

**Update backlog metadata:**
- Increment story counts
- Recalculate effort estimates if applicable

**Save** updated `product/backlog.md`

### 5. Create Release Artifact

**Determine release number:**
- Check `product/iterations/{iteration}/releases/` directory
- Find highest existing release number
- New release is next sequential number

**Create release file:** `product/iterations/{iteration}/releases/release-{number}-{date}.md`

**Content structure:**
```markdown
# Release {number} - {iteration-name}

**Release Date**: {YYYY-MM-DD}
**Iteration**: {iteration-name}
**Release Notes Source**: {path or description}

## Stories Built

### STORY-XXX: {Story Title}
**Status**: Built ✓
**Build Notes**:
{Extract any specific notes about this story from release notes}

### STORY-YYY: {Story Title}
**Status**: Built ✓
**Build Notes**:
{Notes...}

## Stories Moved to Backlog

### STORY-ZZZ: {Story Title}
**Reason**: {Why not built - from user or inferred}
**Action**: Moved to backlog under {priority} priority

## Additional Capabilities Built

{Any capabilities mentioned in release notes that weren't in stories - these need to be captured in product spec}

## Technical Details

{Any notable technical implementation details from release notes worth documenting}

## Metrics

- Stories attempted: {count}
- Stories fully built: {count}
- Stories deferred: {count}
- Build duration: {if available from release notes}
- Release notes: {link or path}

---

*This release artifact provides a historical record of what was built, deferred, and learned during this build increment.*
```

### 6. Update Product Specification

**Read** `product/product-spec.md`

**For each built story:**

a. **Extract capability description** from story:
   - Read the story's "User Story" section
   - Read key acceptance criteria
   - Understand what capability was delivered

b. **Identify appropriate feature area** in product spec:
   - Match story to existing feature area, or
   - Create new feature area if needed

c. **Add capability to feature area:**
   - Under "Capabilities" section, add bullet describing what users can now do
   - Under "User Experience" section, enhance narrative if needed
   - Note any technical implementation details in "Notable Implementation Details"

d. **Update appendix:**
   - Add story to appropriate feature area in "Appendix: Built Stories"
   - Format: `- **STORY-XXX**: {title} (Built: {YYYY-MM-DD})`

**Incorporate additional capabilities:**
- If release notes mention capabilities not in stories, add them
- Flag these for potential story creation in future iterations

**Update metadata:**
- Update "Last Updated" date
- Update version if using semantic versioning

**Save** updated `product/product-spec.md`

### 7. Handle Edge Cases

**Partial story completion:**
- If release notes indicate story partially built, ask user how to handle
- Options: Leave as Ready, split into two stories, or note partial completion

**Stories with dependencies:**
- If unbuilt story was blocked by dependency, note this when adding to backlog

**Technical debt or changes:**
- Capture any technical debt mentioned in release notes
- Note architectural changes or decisions in product spec

## Quality Checks

Before completing reconciliation:

- [ ] All stories in release notes are marked Built
- [ ] All Built stories have Build Date
- [ ] Unbuilt Ready stories handled (backlog or left in iteration)
- [ ] Release artifact created and comprehensive
- [ ] Product spec updated with all new capabilities
- [ ] Product spec appendix includes all newly built stories
- [ ] Backlog updated if stories moved
- [ ] No orphaned or inconsistent story statuses

## Output Summary

After reconciliation, provide summary:

```
## Reconciliation Complete

**Release**: {number} for iteration {iteration-name}

**Stories Built**: {count}
- STORY-XXX: {title}
- STORY-YYY: {title}
- STORY-ZZZ: {title}

**Stories Moved to Backlog**: {count}
- STORY-AAA: {title} (Reason: {reason})
- STORY-BBB: {title} (Reason: {reason})

**Stories Still Ready in Iteration**: {count}
{List any Ready stories not built and not moved to backlog}

**Product Spec Updates**:
- Added {count} new capabilities across {count} feature areas
- Updated {count} feature area narratives
- Appendix now includes {total} built stories

**Files Updated**:
- {count} story files updated to Built status
- product/backlog.md (if applicable)
- product/product-spec.md
- product/iterations/{iteration}/releases/release-{number}-{date}.md

**Next Steps**:
- Review product spec for accuracy
- Consider which backlog stories to include in next build
- Update story map if using Miro for visualization
```

## Notes

- Reconciliation should be run after each build increment
- Product spec should always reflect current product state
- Release artifacts provide audit trail
- Backlog is living document - prioritization can change
- Story status changes are permanent - Built stories don't revert to Ready
