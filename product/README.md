# PRODUCT Directory

This directory supports **iterative, AI-accelerated product discovery and specification**.

## Table of Contents
- [Overview](#overview)
- [Directory Structure](#directory-structure)
- [Initial Setup](#initial-setup)
- [Using with Claude Code](#using-with-claude-code)
  - [Interactive Mode (Recommended)](#interactive-mode-recommended)
  - [CLI Mode](#cli-mode)
- [Workflows](#workflows)
- [Interactive Mode Quick Reference](#interactive-mode-quick-reference)
- [Tips for Success](#tips-for-success)
- [Complete Iteration Example](#complete-iteration-example)
- [Troubleshooting](#troubleshooting)
- [Maintenance](#maintenance)

---

## Overview

This system supports **multiple concurrent iterations** with full traceability:

1. **Start an iteration** - Create iteration-specific directories for all artifacts
2. **Conduct research** - Interviews, observations, surveys
3. **Synthesize findings** - Generate synthesis with cross-iteration references
4. **Extract user stories** - Create stories with comprehensive acceptance criteria
5. **Create story map** - Visualize stories in Miro for planning
6. **Sync priorities** - Update story priorities from Miro collaboration
7. **Load to tracker** - Import to Jira via MCP
8. **Reconcile releases** - Process release notes, update Product Specification

### What is an Iteration?

**Iterations are NOT time-boxed sprints**. They are:
- **Arbitrary length** - Could be days, weeks, or months
- **Initiative-focused** - Bound to a feature area or business goal
- **Concurrent** - Multiple iterations can be active simultaneously
- **Context containers** - Keep LLM context manageable by limiting scope

### Directory Purpose
- **iterations/**: All artifacts for each iteration (discovery, stories, designs)
- **context/**: Core product knowledge that informs all AI-generated work
- **prompts/**: Reusable Claude Code prompts for workflows
- **templates/**: Templates for stories, synthesis, interviews, etc.
- **rules/**: LLM prompting rules aligned with engineering team patterns
- **backlog.md**: Cross-iteration backlog of Ready stories not yet built
- **product-spec.md**: Current product capabilities (updated via `/rel`)
- **artifacts/**: AI-generated outputs and timing logs

---

## Directory Structure

```
product/
├── README.md                          # This file (complete guide)
│
├── iterations/                        # All iteration artifacts
│   ├── 2025-11-mvp/                   # Example iteration (YYYY-MM-name)
│   │   ├── discovery/                 # User research
│   │   │   ├── interviews/
│   │   │   ├── observations/
│   │   │   ├── synthesis/             # Synthesis documents by date
│   │   │   └── README.md
│   │   ├── stories/                   # User stories for this iteration
│   │   │   ├── story-019-*.md
│   │   │   ├── story-020-*.md
│   │   │   └── archive/               # Archived stories
│   │   ├── story-maps/                # Miro story map sync
│   │   │   ├── miro-metadata.json
│   │   │   └── story-map.md
│   │   ├── design/                    # Design artifacts
│   │   │   └── screenshots/
│   │   └── timing.json                # Performance metrics
│   │
│   └── 2025-12-analytics/             # Another iteration
│       └── ...
│
├── releases/                          # Release artifacts (cross-iteration, via /rel)
│   └── release-001-*.md
│
├── backlog.md                         # Ready stories not yet built
├── product-spec.md                    # Current product capabilities
│
├── context/                           # Foundational product knowledge
│   ├── product-overview.md
│   ├── target-users.md
│   ├── technical-context.md
│   ├── competitive-landscape.md
│   └── glossary.md
│
├── templates/                         # Reusable templates
│   ├── story-template-llm-dev.md      # For LLM-centric development
│   ├── story-template-human-dev.md    # For human-centric development
│   ├── interview-template.md
│   ├── synthesis-template.md
│   ├── product-spec-template.md
│   └── rule-template.md
│
├── prompts/                           # Reusable Claude Code prompts
│   ├── synthesize-discovery.md        # Iteration synthesis
│   ├── extract-user-stories.md        # Generate stories + acceptance criteria
│   ├── create-story-map.md            # Create Miro visualization
│   ├── load-stories-to-tracker.md     # Import stories to Jira via MCP
│   ├── release-and-update-spec.md     # Process releases, update spec
│   └── generate-acceptance-criteria.md
│
├── rules/                             # LLM prompting rules
│   └── README.md
│
└── artifacts/                         # Generated outputs
    ├── timing-log.jsonl               # Global timing metrics
    └── designs/
```

---

## Initial Setup

### Step 1: Fill in Product Context

Before doing any discovery synthesis, populate these files with what you know:

1. `context/product-overview.md` - Your product vision and goals
2. `context/target-users.md` - Who you're building for
3. `context/technical-context.md` - Your tech stack and constraints

These files provide essential context for AI to generate relevant, accurate outputs.

### Step 2: Start Your First Iteration

Organize work by iterations using the `/iter` slash command:

**Start a Claude Code session:**
```bash
cd /path/to/your/project
claude-code
```

**Then use the `/iter` command:**
```
/iter
```

You'll be prompted for:
- Iteration name (e.g., "mvp", "dark-mode", "analytics-dashboard")
- Description (e.g., "Build core feedback collection functionality")
- Whether to conduct an immediate interview

This creates:
- `product/iterations/YYYY-MM-{name}/` directory
- Subdirectories for discovery, stories, releases, story-maps, design
- A README to track iteration goals and progress
- Optional: formatted interview notes if you chose to be interviewed
- `timing.json` file to track iteration performance

### Step 3: Capture Discovery Data

As you conduct user research for this iteration:

1. Use the interview template: `product/templates/interview-template.md`
2. Create one file per interview: `iterations/[ITERATION]/discovery/interviews/2025-11-15-participant-001.md`
3. Be specific with quotes, pain points, and workflows
4. Tag insights for easier synthesis

---

## Using with Claude Code

You can use this system in two ways: **Interactive Mode** (recommended) or **CLI Mode**.

### Interactive Mode (Recommended)

Start a Claude Code session and use slash commands or natural language.

**Start session:**
```bash
cd /path/to/your/project
claude-code
```

**Available slash commands:**
- `/iter` - Start a new iteration with optional interview
- `/synth` - Synthesize discovery materials for current iteration
- `/req` - Extract user stories from synthesis
- `/map` - Create Miro story map from stories
- `/demap` - Sync Miro story map priorities back to stories
- `/jira` - Load stories to Jira backlog
- `/rel` - Reconcile release notes and update Product Specification

**Or use natural language commands like:**
```
Synthesize discovery for iteration: 2025-11-mvp
```

See [Interactive Mode Quick Reference](#interactive-mode-quick-reference) below for all commands.

---

## Workflows

### Workflow 1: Start New Iteration

**When**: Beginning work on a new feature area or initiative

**Interactive Mode:**
```
/iter
```

**What it does**:
- Creates iteration directory structure
- Initializes README with goals and timeline
- Optionally conducts structured interview
- Records timing data

**Output**: Complete iteration directory ready for discovery work

---

### Workflow 2: Synthesize User Research

**When**: After completing 5-10 user interviews for an iteration

**Interactive Mode:**
```
/synth
```

**What it does**:
- Analyzes all interview files for this iteration
- Identifies themes and patterns
- Extracts user needs
- Proposes features with evidence
- Cross-references previous iterations
- Creates synthesis document

**Output**: `product/iterations/{iteration}/discovery/synthesis/synthesis-{date}.md`

---

### Workflow 3: Extract User Stories with Acceptance Criteria

**When**: After creating a synthesis document for an iteration

**Interactive Mode:**
```
/req
```

**What it does**:
- Converts synthesis insights into user stories
- Generates comprehensive acceptance criteria (Given-When-Then)
- Uses appropriate template (LLM-dev or human-dev)
- Ensures sequential story numbering across all iterations
- Formats stories properly (As a... I want... So that...)
- Estimates effort

**Output**:
- New story files in `product/iterations/{iteration}/stories/`
- Each story has complete acceptance criteria
- Stories ready for /map or /jira

---

### Workflow 4: Create Story Map

**When**: After extracting stories, to visualize and plan releases

**Interactive Mode:**
```
/map
```

**What it does**:
- Creates visual story map in Miro
- Organizes stories by user activities
- Applies swim lanes for prioritization (NOW/NEXT/LATER)
- Color-codes by story type
- Adds persona emojis
- Saves metadata for future syncing

**Output**:
- Miro board with production-grade formatting
- `product/iterations/{iteration}/story-maps/miro-metadata.json`
- `product/iterations/{iteration}/story-maps/story-map.md`

**Note**: Requires Miro MCP to be configured

---

### Workflow 5: Sync Story Map Priorities

**When**: After team collaboration on Miro board adjusts priorities

**Interactive Mode:**
```
/demap
```

**What it does**:
- Reads current Miro board state
- Detects swim lane positions (NOW/NEXT/LATER)
- Updates story file metadata with current priorities
- Handles new stories added to Miro (asks for details)
- Handles removed stories (offers to archive or move to backlog)
- Updates miro-metadata.json with sync history

**Output**:
- Updated story files with latest priorities
- Summary of changes (X updated, Y added, Z archived)

---

### Workflow 6: Load Stories to Jira

**When**: After stories are extracted and prioritized

**Interactive Mode:**
```
/jira
```

**What it does**:
- Reads story markdown files for current iteration
- Extracts title, description, acceptance criteria, priority
- Creates issues in Jira via Atlassian MCP
- No epic parent (stories are standalone)
- Uses labels to group stories from same iteration

**Output**:
- Issues created in Jira
- Summary with issue keys
- Direct links to view in Jira

---

### Workflow 7: Reconcile Releases

**When**: After a build increment is deployed to production

**Interactive Mode:**
```
/rel
```

**What it does**:
- Parses release notes for story IDs
- Updates story statuses: Ready → Built
- Identifies unbuilt Ready stories (asks about moving to backlog)
- Creates release artifact in `product/releases/`
- Updates Product Specification with newly built capabilities
- Updates backlog.md if stories moved

**Output**:
- Updated story files with Built status
- Release artifact documenting what was built
- Updated product-spec.md
- Updated backlog.md (if applicable)

---

## Interactive Mode Quick Reference

### Starting a Session

```bash
cd product
claude-code
```

### Common Commands

| Task | Slash Command | Natural Language Alternative |
|------|---------------|------------------------------|
| Start iteration | `/iter` | N/A (use slash command) |
| Synthesize | `/synth` | `Synthesize discovery for iteration: [NAME]` |
| Generate stories | `/req` | `Extract stories from iteration: [NAME]` |
| Create story map | `/map` | `Create story map for iteration: [NAME]` |
| Sync Miro priorities | `/demap` | `Sync Miro priorities for iteration: [NAME]` |
| Load to Jira | `/jira` | `Load stories for iteration: [NAME] to Jira` |
| Reconcile release | `/rel` | `Reconcile release notes for iteration: [NAME]` |

### Story Lifecycle

Stories follow this lifecycle:

```
Draft → Ready → Built
         ↓
      Backlog (if not built in iteration)
         ↓
      Archived (if removed from scope)
```

**Story statuses**:
- **Draft**: Story created but needs refinement
- **Ready**: Story ready for development
- **Built**: Story implemented and deployed
- **Backlog**: Ready story moved to backlog for future work
- **Archived**: Story removed from scope

---

## Tips for Success

### Managing Iterations
- **Name iterations clearly**: Format is `YYYY-MM-initiative-name`
- **One focus per iteration**: Don't try to explore everything at once
- **Concurrent iterations OK**: Multiple teams can work on different iterations
- **Stories stay in iterations**: Easier for humans to navigate, smaller LLM context

### For Better Context
- Keep context files updated as product evolves
- Be specific in discovery notes (exact quotes > paraphrasing)
- Tag and categorize insights consistently

### For Better AI Outputs
- Provide multiple interviews (5+ recommended) per iteration
- Include specific evidence in interview files
- Reference user personas consistently
- Update prompts based on what works for your team

### File Organization
- **Active iterations**: Keep in `iterations/{name}/`
- **Story numbering**: Sequential across all iterations (never reuse numbers)
- **Backlog management**: Use `product/backlog.md` for cross-iteration Ready stories
- **Archives**: Use `stories/archive/{date}-demap/` for removed stories

---

## Complete Iteration Example

### Week 1: Start Iteration

**Using slash command:**
```
/iter
```

Then provide:
- Iteration name: `dark-mode`
- Description: `Add dark mode support to conference survey`
- Interview: `yes` (to conduct immediate interview)

### Weeks 1-2: Conduct Research
- Interview 5-8 users
- Document in `iterations/2025-12-dark-mode/discovery/interviews/`
- Update iteration README with progress

### Week 3: Synthesize

**Using slash command:**
```
/synth
```
(Auto-detects iteration, creates synthesis with timing)

**Result:**
- Synthesis created in `discovery/synthesis/synthesis-{date}.md`
- Timing recorded in iteration's `timing.json`

### Week 3-4: Extract Stories

**Using slash command:**
```
/req
```
(Auto-detects iteration, determines story numbering, extracts stories)

**Result:**
- Stories generated in `stories/` directory
- Complete acceptance criteria included
- Timing recorded

### Week 4: Create Story Map

**Using slash command:**
```
/map
```
(Creates Miro board from stories)

**Result:**
- Miro board with visual story map
- Metadata saved for future syncing

### Week 4: Collaborate & Sync

- Team adjusts priorities on Miro board
- Run `/demap` to sync changes back to story files

### Week 4: Load to Jira

**Using slash command:**
```
/jira
```
(Loads all stories for iteration to Jira)

**Result:**
- Stories created in Jira with latest priorities
- All acceptance criteria included

### Ongoing: Build & Deploy

- Development team builds stories
- Release to production

### After Release: Reconcile

**Using slash command:**
```
/rel
```
(Parses release notes, updates story statuses, updates Product Spec)

**Result:**
- Stories marked as Built
- Product Specification updated with new capabilities
- Release artifact created

---

## Troubleshooting

### If story generation fails

**Interactive:**
```
Read the synthesis and tell me what potential stories you see
```

Then manually request specific stories:
```
Create a user story for [FEATURE] with comprehensive acceptance criteria
```

### If Miro sync fails

Check that:
- Miro MCP is configured
- Board ID is correct in miro-metadata.json
- Swim lane separators are in place

### Check what exists

```
List all iterations in product/iterations/
```

```
Show me the most recent synthesis file
```

```
What's the next available story ID?
```

---

## Maintenance

- Update context files when product direction changes
- Run `/demap` after Miro collaboration sessions
- Run `/rel` after each production release
- Create meta-synthesis when patterns emerge across iterations
- Archive old iterations (>6 months) to `iterations/archive/`

---

## Getting Help

- **See available prompts**: `ls product/prompts/`
- **Read a prompt**: Ask to see any prompt file
- **Understand structure**: "Explain the directory structure"
- **Check status**: "What iterations do we have and which are active?"

---

## Next Steps

1. ✅ Fill in `context/` files
2. ✅ Run `/iter` to start your first iteration
3. ✅ Conduct interviews
4. ✅ Run `/synth` to create synthesis
5. ✅ Run `/req` to extract stories
6. ✅ Run `/map` to create story map
7. ✅ Run `/demap` after Miro collaboration
8. ✅ Run `/jira` to load to backlog
9. ✅ Build and release
10. ✅ Run `/rel` to reconcile and update Product Spec

---

**Remember**: This is an iterative system. Each iteration builds on previous learning!

In interactive mode, you can be conversational. Claude understands context and can help guide you through the workflows!
