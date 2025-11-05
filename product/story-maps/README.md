# Story Maps Directory

This directory contains **story map** artifacts that visualize user journeys and organize stories by user activities and personas.

## Purpose

Story maps help teams:
1. **Visualize the user journey** - See the complete end-to-end experience
2. **Find gaps** - Identify missing steps or stories in the journey
3. **Prioritize releases** - Organize stories into walking skeleton + iterations
4. **Collaborate visually** - Enable stakeholders to contribute in Miro

## Important: Miro Board Creation

**⚠️ Miro Limitation**: Boards cannot be created via API/MCP. You must manually create boards in the Miro web interface before using them.

**Before running `/map`**:
1. Go to [miro.com](https://miro.com)
2. Create a new board
3. Name it: `Story Map - YYYY-MM-DD - [Name]`
4. Note the board ID from the URL

**Example board names**:
- `Story Map - 2025-11-04 - Iteration-1`
- `Story Map - 2025-11-15 - Dark-Mode`

See `BOARD-NAMING-CONVENTION.md` for complete guidelines.

---

## Workflow Integration

Story maps can be created at various points in the discovery cycle:

### Option 1: From Synthesis (Before Story Extraction)
1. **Create Miro board** manually (see above)
2. Run `/synth` to create synthesis document
3. Run `/map` to generate visual story map in Miro from synthesis
4. Team reviews map, identifies gaps, refines journey
5. Run `/req` to extract stories (informed by map)

### Option 2: From Extracted Stories (Organization)
1. Run `/req` to extract stories from synthesis
2. **Create Miro board** manually (see above)
3. Run `/map` to organize existing stories into journey on Miro
4. Team reviews map, finds gaps, adjusts priorities
5. Add any missing stories identified during mapping

### Option 3: From Miro Workshop (Human-First)
1. **Create Miro board** manually (see above)
2. Team creates story map in Miro workshop
3. Run `/map` with sync direction: Miro→Markdown
4. AI reads Miro board and generates story files
5. Stories are synced to `requirements/` directory
6. Run `/jira` to load stories to backlog

## Directory Structure

```
story-maps/
├── README.md                          # This file
├── story-map-template.md              # Template for story map documents
├── 2025-10-30-Iteration-1/
│   ├── story-map.md                   # Journey visualization
│   ├── miro-metadata.json             # Sync metadata
│   └── journey-insights.md            # Workshop notes
└── 2025-10-30-dark-mode/
    └── story-map.md
```

## File Naming Convention

- Story map directory: Same as discovery cycle name (e.g., `2025-10-30-Iteration-1/`)
- Main file: `story-map.md`
- Metadata: `miro-metadata.json`
- Workshop notes: `journey-insights.md`

## Story Map Format

Each story map includes:

1. **Overview**: Initiative, epic, personas involved
2. **User Journey**: Activities organized by persona
3. **Story Cards**: Organized under each activity
4. **Infrastructure Stories**: Technical dependencies
5. **Release Plan**: Walking skeleton + subsequent releases
6. **Gaps**: Missing stories or deferred features
7. **Sync Metadata**: Miro board mapping for bidirectional sync

## Miro Board Structure

**Standard Layout**:
```
┌─────────────────────────────────────────────────┐
│ [Epic Header - Orange]                          │
└─────────────────────────────────────────────────┘

Persona: [Name]          Persona: [Name]
┌──────────────┐         ┌──────────────┐
│ Activity 1   │         │ Activity 3   │
│ [Blue]       │         │ [Blue]       │
└──────────────┘         └──────────────┘
     │                        │
     ▼                        ▼
┌──────────────┐         ┌──────────────┐
│ STORY-###    │         │ STORY-###    │
│ [Yellow]     │         │ [Yellow]     │
│ Must Have    │         │ Must Have    │
└──────────────┘         └──────────────┘
     │                        │
┌──────────────┐         ┌──────────────┐
│ STORY-###    │         │ STORY-###    │
│ [Green]      │         │ [Green]      │
│ Should Have  │         │ Should Have  │
└──────────────┘         └──────────────┘

┌─────────────────────────────────────────────────┐
│ Release 1: [Name]                               │
│ Release 2: [Name]                               │
└─────────────────────────────────────────────────┘
```

**Color Coding**:
- **Orange**: Epic/Initiative headers
- **Blue**: User activity/step headers
- **Yellow**: Must Have stories
- **Light Green**: Should Have stories
- **Light Pink**: Could Have stories
- **Gray**: Won't Have / Deferred
- **Red**: Infrastructure/Technical dependencies
- **Cyan**: Spike stories (research)

## Sync Strategies

### Markdown → Miro
**When**: You have stories in markdown and want to visualize in Miro
**Process**: AI reads story files, creates/updates Miro board
**Use case**: Organizing extracted stories, release planning

### Miro → Markdown
**When**: Team created/modified story map in Miro
**Process**: AI reads Miro board, creates/updates markdown files
**Use case**: After collaborative workshops, capturing manual changes

### Bidirectional
**Best practice**:
1. Markdown files remain source of truth for story details
2. Miro board is source of truth for journey organization
3. Sync before major activities (grooming, planning, Jira import)

## Using /map Command

### Scenario 1: Create story map from existing stories
```
/map
```
Then provide:
- Cycle: 2025-10-30-Iteration-1
- Miro board: MCP Test 1
- Source: stories
- Personas: New User, Returning User

### Scenario 2: Sync Miro changes back to markdown
```
/map
```
Then provide:
- Cycle: 2025-10-30-Iteration-1
- Sync direction: Miro→Markdown
- Update existing stories: yes

### Scenario 3: Create map from synthesis (before stories exist)
```
/map
```
Then provide:
- Cycle: 2025-10-30-Iteration-1
- Miro board: MCP Test 1
- Source: synthesis
- Extract stories after: yes/no

## Best Practices

### For Better Story Maps
- **One epic per map** - Keep maps focused on a single initiative
- **Clear personas** - Organize activities by who is performing them
- **Verb-based activities** - "Sign Up", "Browse Products", "Check Out"
- **Prioritize vertically** - Must haves at top, nice-to-haves below
- **Walking skeleton first** - Identify minimum viable journey

### For Better Collaboration
- **Run workshops** - Bring team together to build map collaboratively
- **Use Miro real-time** - Enable stakeholders to add cards during discussion
- **Find gaps together** - Map reveals missing steps better than lists
- **Vote on priorities** - Use Miro voting features for priority discussions

### For Better Sync
- **Sync before Jira import** - Ensure markdown reflects latest Miro state
- **Document sync timestamp** - Track when last sync occurred
- **Review changes** - Check what changed during sync before committing
- **Resolve conflicts manually** - If both markdown and Miro changed, human decides

## Integration with Existing Workflow

Story mapping fits into the existing workflow:

```
/cycle → Interviews → /synth → /map → /req → /jira
                                  ↓
                              [Miro Workshop]
                                  ↓
                              /map (sync)
```

Or:

```
/cycle → Interviews → /synth → /req → /map → /jira
                                        ↓
                                   [Organize stories]
                                   [Find gaps]
                                   [Plan releases]
```

## Maintenance

- Update story maps when stories are added/modified
- Re-sync after major Miro workshop sessions
- Archive old maps when initiatives are complete
- Document key decisions made during mapping sessions

---

## Example Story Map

See `2025-10-30-Iteration-1/story-map.md` for a complete example.
