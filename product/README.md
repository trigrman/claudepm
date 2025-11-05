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
- [Complete Cycle Example](#complete-cycle-example)
- [Troubleshooting](#troubleshooting)
- [Maintenance](#maintenance)

---

## Overview

This system supports **multiple discovery cycles** with full traceability:

1. **Start a discovery cycle** - Create cycle-specific directories
2. **Conduct research** - Interviews, observations, surveys
3. **Synthesize findings** - Generate cycle synthesis with cross-cycle references
4. **Extract user stories** - Create or update requirements with comprehensive acceptance criteria
5. **Load to tracker** - Optional import to Jira/Linear via MCP
6. **Track evolution** - Maintain indexes showing which cycle generated what
7. **Meta-synthesis** - Periodically analyze patterns across cycles

### Directory Purpose
- **context/**: Core product knowledge that informs all AI-generated work
- **discovery/**: User research organized by discovery cycles, with meta-synthesis
- **requirements/**: Epics, user stories, and acceptance criteria (tracked by cycle)
- **prompts/**: Reusable Claude Code prompts for common workflows
- **artifacts/**: AI-generated outputs

---

## Directory Structure

```
product/
├── README.md                          # This file (complete guide)
│
├── context/                           # Foundational product knowledge
│   ├── product-overview.md
│   ├── target-users.md
│   ├── technical-context.md
│   ├── competitive-landscape.md
│   └── glossary.md
│
├── discovery/                         # User research organized by cycles
│   ├── interview-template.md          # Template for interviews
│   ├── synthesis-template.md          # Template for synthesis
│   ├── 2025-01-15-onboarding/        # Example cycle (YYYY-MM-DD format)
│   │   ├── README.md                  # Cycle goals and progress
│   │   ├── interviews/
│   │   │   └── 2025-01-15-participant-001.md
│   │   ├── observations/
│   │   ├── surveys/
│   │   └── synthesis-2025-01-20.md
│   ├── 2025-02-10-notifications/     # Another cycle
│   │   └── ...
│   └── meta-synthesis/               # Cross-cycle analysis
│       ├── meta-synthesis-template.md
│       └── meta-2025-q1.md
│
├── requirements/                      # Output: What to build
│   ├── stories-by-cycle.md            # Index of stories by cycle
│   ├── story-template.md              # Template for user stories
│   ├── epic-template.md               # Template for epics
│   ├── 2025-01-15-onboarding/        # Requirements for cycle
│   │   ├── story-001-user-login.md
│   │   ├── story-002-dashboard.md
│   │   └── epic-001-onboarding.md
│   └── 2025-02-10-notifications/     # Another cycle
│       └── story-010-push-notifications.md
│
├── prompts/                          # Reusable Claude Code prompts
│   ├── synthesize-discovery.md       # Cycle synthesis
│   ├── extract-user-stories.md       # Generate stories + acceptance criteria
│   ├── load-stories-to-tracker.md    # Import stories to Jira/Linear via MCP
│   └── create-meta-synthesis.md      # Cross-cycle analysis
│
└── artifacts/                        # Generated outputs from AI
```

---

## Initial Setup

### Step 1: Fill in Product Context

Before doing any discovery synthesis, populate these files with what you know:

1. `context/product-overview.md` - Your product vision and goals
2. `context/target-users.md` - Who you're building for
3. `context/technical-context.md` - Your tech stack and constraints

These files provide essential context for AI to generate relevant, accurate outputs.

### Step 2: Start Your First Discovery Cycle

Instead of dumping all research in one place, organize by discovery cycles using the `/cycle` slash command:

**Start a Claude Code session:**
```bash
cd /Users/mike/dev/nam-demo
claude-code
```

**Then use the `/cycle` command:**
```
/cycle
```

You'll be prompted for:
- Cycle name (e.g., "onboarding-flow")
- Description (e.g., "Understanding user onboarding pain points")
- Whether to conduct an immediate interview

This creates:
- `product/discovery/YYYY-MM-DD-{name}/` directory (e.g., `2025-10-30-onboarding-flow/`)
- Subdirectories for interviews, observations
- A README to track cycle goals and progress
- Optional: formatted interview notes if you chose to be interviewed
- `timing.json` file to track cycle performance

### Step 3: Capture Discovery Data

As you conduct user research for this cycle:

1. Use the interview template: `discovery/[CYCLE-NAME]/interviews/interview-template.md`
2. Create one file per interview: `discovery/[CYCLE-NAME]/interviews/2025-10-15-participant-001.md`
3. Be specific with quotes, pain points, and workflows
4. Tag insights for easier synthesis

---

## Using with Claude Code

You can use this system in two ways: **Interactive Mode** (recommended) or **CLI Mode**.

### Interactive Mode (Recommended)

Start a Claude Code session and use slash commands or natural language.

**Start session:**
```bash
cd /Users/mike/dev/nam-demo
claude-code
```

**Available slash commands:**
- `/cycle` - Start a new discovery cycle with optional interview
- `/synth` - Synthesize discovery materials for current cycle
- `/req` - Extract user stories and epic from synthesis
- `/jira` - Load stories to Jira backlog

**Or use natural language commands like:**
```
Synthesize discovery for cycle: 2025-10-onboarding-flow
```

See [Interactive Mode Quick Reference](#interactive-mode-quick-reference) below for all commands.

### CLI Mode

Execute workflows from the command line with explicit context.

**Synthesize discovery research (for a specific cycle):**
```bash
CYCLE="2025-10-onboarding-flow"

claude-code --context product/context/* \
  --context product/discovery/$CYCLE/interviews/* \
  --context product/discovery/$CYCLE/observations/* \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/synthesize-discovery.md
```

**Extract user stories (from cycle synthesis):**
```bash
CYCLE="2025-10-onboarding-flow"

claude-code --context product/context/product-overview.md \
  --context product/context/target-users.md \
  --context product/context/technical-context.md \
  --context product/discovery/$CYCLE/synthesis-*.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/extract-user-stories.md
```

**Create meta-synthesis (across multiple cycles):**
```bash
claude-code --context product/discovery/2025-*/synthesis-*.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/create-meta-synthesis.md
```

---

## Workflows

### Workflow 1: Synthesize User Research (For a Discovery Cycle)

**When**: After completing 5-10 user interviews for a cycle

**Interactive Mode:**
```
Synthesize discovery for cycle: 2025-10-onboarding-flow
```

**CLI Mode:**
```bash
CYCLE="2025-10-onboarding-flow"

claude-code --context product/context/* \
  --context product/discovery/$CYCLE/interviews/* \
  --context product/discovery/$CYCLE/observations/* \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/synthesize-discovery.md
```

**What it does**:
- Analyzes all interview files for this cycle
- Identifies themes and patterns
- Extracts user needs
- Proposes features with evidence
- **Cross-references previous cycles** to note confirming/contradicting findings
- Creates synthesis document

**Output**: `product/discovery/[CYCLE-NAME]/synthesis-[date].md`

**After synthesis**:
1. Note if any findings contradict previous research

---

### Workflow 2: Extract User Stories with Acceptance Criteria

**When**: After creating a synthesis document for a cycle

**Interactive Mode:**
```
Extract stories from cycle: 2025-10-onboarding-flow, starting at story 001
```

**CLI Mode:**
```bash
CYCLE="2025-10-onboarding-flow"

claude-code --context product/context/product-overview.md \
  --context product/context/target-users.md \
  --context product/context/technical-context.md \
  --context product/discovery/$CYCLE/synthesis-*.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/extract-user-stories.md
```

**What it does**:
- Converts synthesis insights into user stories
- **Generates comprehensive acceptance criteria** for each story:
  - Given-When-Then scenarios (happy path, errors, edge cases)
  - Non-functional requirements (performance, security, accessibility)
  - Quality checklist
- **Checks for existing similar stories** to avoid duplication
- Formats stories properly (As a... I want... So that...)
- Estimates effort
- Maintains traceability to discovery cycle
- Updates existing stories if new findings refine them
- **Formats stories for easy import** to issue trackers

**Output**:
- New story files in `product/requirements/[CYCLE-NAME]/`
- Each story has complete acceptance criteria ready for development
- Stories formatted for Jira/Linear/etc. import via MCP
- Updated `stories-by-cycle.md` with this cycle's stories

**After story extraction**:
1. Update `stories-by-cycle.md` with new stories and cycle info
2. If stories were updated, document changes in the story's "Change History"
3. *Optional*: Load stories to issue tracker (see Workflow 2b)

---

### Workflow 2b: Load Stories to Issue Tracker (Optional)

**When**: After generating stories with acceptance criteria

**Interactive Mode:**
```
Load stories 001-005 to Jira project PROD
```

**CLI Mode:**
```bash
CYCLE="2025-10-onboarding-flow"

claude-code --context product/requirements/$CYCLE/story-001-*.md \
  --context product/requirements/$CYCLE/story-002-*.md \
  --context product/requirements/$CYCLE/story-003-*.md \
  product/prompts/load-stories-to-tracker.md
```

**What it does**:
- Reads story markdown files
- Extracts title, description, acceptance criteria, labels, priority
- Creates issues in your tracker (Jira, Linear, etc.) via MCP
- Maps priorities and fields appropriately
- Provides summary of created issues with their keys/IDs

**Output**:
- Issues created in your tracker
- Summary mapping story files to issue keys
- List of any failures for troubleshooting

**Usage notes**:
- Test with 2-3 stories first to verify formatting
- Story markdown files remain the source of truth
- You can optionally update story files with tracker issue keys after import

---

### Workflow 3: Meta-Synthesis (Cross-Cycle Analysis)

**When**: Quarterly, or when you have 3+ related cycles

**Interactive Mode:**
```
Create meta-synthesis for Q1 2025
```

**CLI Mode:**
```bash
claude-code --context product/discovery/2025-01-*/synthesis-*.md \
  --context product/discovery/2025-02-*/synthesis-*.md \
  --context product/discovery/2025-03-*/synthesis-*.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/create-meta-synthesis.md
```

**What it does**:
- Identifies themes across multiple cycles
- Tracks how understanding evolved
- Finds contradictions and patterns
- Validates or invalidates assumptions
- Provides strategic product direction

**Output**: `product/discovery/meta-synthesis/meta-[timeperiod].md`

**Use for**:
- Roadmap planning
- Strategic product decisions
- Identifying research gaps
- Feature prioritization

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
| Start cycle | `/cycle` | N/A (use slash command) |
| Synthesize | `/synth` | `Synthesize discovery for cycle: [NAME]` |
| Generate stories | `/req` | `Extract stories from cycle: [NAME], starting at story [ID]` |
| Load to Jira | `/jira` | `Load stories [IDs] to Jira project [KEY]` |
| Meta-synthesis | N/A | `Create meta-synthesis for Q[N] [YEAR]` |
| Check duplicates | N/A | `Do we have stories similar to [DESCRIPTION]?` |

### Detailed Command Examples

#### 1. Start a New Discovery Cycle

**Using slash command:**
```
/cycle
```

Then answer the prompts:
- Cycle name: `mobile-onboarding`
- Description: `Understanding first-time mobile user experience`
- Interview: `yes` or `no`

**What happens**:
- Creates cycle directory structure
- Initializes README with goals and timeline
- Optionally conducts structured interview
- Records timing data
- Shows next steps

---

#### 2. Synthesize Discovery Research

**Using slash command:**
```
/synth
```
(Auto-detects current cycle or prompts you to specify)

**Or natural language:**
```
Synthesize discovery for cycle: 2025-10-mobile-onboarding
```

**Full:**
```
Please synthesize the discovery research for the 2025-10-mobile-onboarding cycle.

Read:
- product/context/*
- product/discovery/2025-10-mobile-onboarding/interviews/*
- product/discovery/2025-10-mobile-onboarding/observations/*
- product/requirements/stories-by-cycle.md

Follow the instructions in product/prompts/synthesize-discovery.md
```

---

#### 3. Extract User Stories with Acceptance Criteria

**Using slash command:**
```
/req
```
(Auto-detects current cycle, determines next story number automatically)

**Or natural language:**
```
Extract stories from cycle: 2025-10-mobile-onboarding, starting at story 001
```

**Full:**
```
Please extract user stories with acceptance criteria from the 2025-10-mobile-onboarding synthesis.

Discovery Cycle: 2025-10-mobile-onboarding
Starting Story ID: 001

Read:
- product/context/product-overview.md
- product/context/target-users.md
- product/context/technical-context.md
- product/discovery/2025-10-mobile-onboarding/synthesis-*.md
- product/requirements/user-stories/stories-by-cycle.md
- product/discovery/INDEX.md

Follow the instructions in product/prompts/extract-user-stories.md
```

**After:**
```
Update product/requirements/stories-by-cycle.md with the new stories from this cycle
```

---

#### 4. Load Stories to Jira

**Using slash command:**
```
/jira
```
(Auto-detects current cycle, loads all stories with epic links)

**Or natural language:**
```
Load stories 001-005 to Jira project PROD
```

**Full:**
```
Please load these stories to Jira:
- product/requirements/2025-10-mobile-onboarding/story-001-*.md
- product/requirements/2025-10-mobile-onboarding/story-002-*.md
- product/requirements/2025-10-mobile-onboarding/story-003-*.md

Project Key: PROD
Issue Type: Story

Follow the instructions in product/prompts/load-stories-to-tracker.md
```

**Test first:**
```
Load only story-001 to Jira project PROD to test the formatting
```

---

#### 5. Create Meta-Synthesis

**Quick:**
```
Create meta-synthesis for Q1 2025
```

**Full:**
```
Please create a meta-synthesis across all Q1 2025 discovery cycles.

Read:
- product/discovery/INDEX.md
- product/discovery/2025-01-*/synthesis-*.md
- product/discovery/2025-02-*/synthesis-*.md
- product/discovery/2025-03-*/synthesis-*.md
- product/requirements/user-stories/stories-by-cycle.md

Follow the instructions in product/prompts/create-meta-synthesis.md
```

---

### Update Commands

```
Update story-003 based on findings from the 2025-10-analytics-dashboard cycle synthesis
```

```
Update product/requirements/stories-by-cycle.md with stories 011-015 from the analytics-dashboard cycle
```

---

### Exploration Commands

```
Show me all stories from the onboarding cycles
```

```
What stories do we have related to mobile experience?
```

```
Summarize the key findings from the 2025-10-mobile-onboarding synthesis
```

```
Before creating a new story about user profile editing, check if we already have similar stories
```

---

### Example Interactive Session

```
User: /cycle

Claude: [Prompts for cycle name, description, interview preference]

User: payment-flow
      Understanding payment pain points
      yes

Claude: [Conducts interview, creates cycle structure, records timing]

User: I've added some technical observations. /synth

Claude: [Reads all discovery materials, creates synthesis (e.g., 5 minutes)]

User: /req

Claude: [Extracts epic and stories with acceptance criteria (e.g., 7 minutes)]

User: /jira

Claude: [Creates epic SCRUM-65, creates 6 stories SCRUM-66-71, links all (e.g., 8 minutes)]

User: Show me the total time for this cycle

Claude: [Reports 20 minutes from cycle start to Jira backlog]
```

---

## Tips for Success

### Managing Discovery Cycles
- **Name cycles clearly**: Format is `YYYY-MM-DD-initiative-name` (automatically created by script)
- **One focus per cycle**: Don't try to explore everything at once
- **Update stories-by-cycle.md**: Maintain traceability from discovery to requirements

### For Better Context
- Keep context files updated as product evolves
- Be specific in discovery notes (exact quotes > paraphrasing)
- Tag and categorize insights consistently
- **Always include stories-by-cycle.md** in context for cross-cycle awareness

### For Better AI Outputs
- Provide multiple interviews (5+ recommended) per cycle
- Include specific evidence in interview files
- Reference user personas consistently
- Update prompts based on what works for your team
- **Run meta-synthesis quarterly** to identify strategic patterns

### File Organization
- **Active cycles**: Keep in `discovery/[CYCLE-NAME]/`
- **Archive old cycles**: Move to `discovery/cycles-archive/` after 6 months
- Version specifications as they change
- Use clear, descriptive filenames
- Link related files (stories → cycles → synthesis)

### Interactive Mode Tips

#### 1. Let Claude Explore
You don't need to specify every file:
```
✅ "Synthesize the mobile-onboarding cycle"
❌ "Read product/discovery/2025-10-mobile-onboarding/interviews/interview-001.md, then read..."
```

#### 2. Be Specific About Inputs
Do provide key parameters:
```
✅ "Extract stories from mobile-onboarding, starting at story 011, project key PROD"
❌ "Extract some stories"
```

#### 3. Iterate and Refine
```
"The acceptance criteria for story-002 need more security requirements. Please enhance them."
```

#### 4. Ask for Summaries
```
"Summarize what stories we generated from this cycle"
"What are the main themes across all our Q1 cycles?"
```

#### 5. Reference Previous Context
```
"Using the same format as story-001, create a story for password reset"
```

---

## Complete Cycle Example

Here's how a full cycle works:

### Week 1: Start Cycle

**Using slash command:**
```
/cycle
```

Then provide:
- Cycle name: `mobile-onboarding`
- Description: `Mobile app first-time user experience`
- Interview: `yes` (to conduct immediate interview)

### Weeks 1-2: Conduct Research
- Interview 5-8 users
- Document in `discovery/2025-10-mobile-onboarding/interviews/`
- Update cycle README with progress

### Week 3: Synthesize

**Using slash command:**
```
/synth
```
(Auto-detects cycle, creates synthesis with timing)

**Or CLI:**
```bash
CYCLE="2025-10-mobile-onboarding"
claude-code --context product/context/* \
  --context product/discovery/$CYCLE/interviews/* \
  --context product/discovery/INDEX.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/synthesize-discovery.md
```

**Result:**
- Synthesis created in ~5 minutes
- Timing recorded in cycle's `timing.json`
- Note any cross-cycle patterns

### Week 3-4: Extract Stories

**Using slash command:**
```
/req
```
(Auto-detects cycle, determines story numbering, extracts epic and stories)

**Or CLI:**
```bash
claude-code --context product/context/* \
  --context product/discovery/$CYCLE/synthesis-*.md \
  --context product/requirements/stories-by-cycle.md \
  product/prompts/extract-user-stories.md
```

**Result:**
- Epic and stories generated in ~7 minutes
- Complete acceptance criteria included
- `stories-by-cycle.md` updated automatically
- Timing recorded

### Week 4: Load to Jira (Optional)

**Using slash command:**
```
/jira
```
(Auto-detects cycle, loads epic and all stories with proper parent links)

**Or CLI:**
```bash
CYCLE="2025-10-mobile-onboarding"
claude-code --context product/requirements/$CYCLE/story-*.md \
  product/prompts/load-stories-to-tracker.md
```

**Result:**
- Epic and stories created in Jira in ~8 minutes
- All stories linked to epic
- All acceptance criteria included
- Timing recorded

### Ongoing: Prioritize & Build
- Use stories for sprint planning
- Engineering team adds technical specifications to stories as needed

### Quarterly: Meta-Synthesis
- Analyze patterns across all Q1 cycles
- Inform roadmap planning

---

## Troubleshooting

### If story generation fails

**Interactive:**
```
Read the synthesis at product/discovery/[CYCLE]/synthesis-[DATE].md and tell me what potential stories you see
```

Then manually request specific stories:
```
Create a user story for [FEATURE] with comprehensive acceptance criteria following the template
```

### If tracker import fails

**Interactive:**
```
Show me the formatted description for story-001 as it would appear in Jira
```

Then manually create or fix the issue.

### Check what exists

```
List all discovery cycles in product/discovery/
```

```
Show me the most recent synthesis file
```

```
What's the next available story ID according to stories-by-cycle.md?
```

### Working with MCP Tools

When loading to Jira via Atlassian MCP, Claude will automatically:
- Get your cloud ID
- Check project types
- Map priorities
- Create issues
- Handle errors

You just need to provide:
- Project key (e.g., "PROD")
- Issue type (e.g., "Story")
- Which stories to load

---

## Maintenance

- Update context files when product direction changes
- Update `discovery/INDEX.md` after each cycle
- Update `stories-by-cycle.md` when generating requirements
- Create meta-synthesis quarterly or when patterns emerge
- Archive old cycles (>6 months) to `discovery/cycles-archive/`

---

## Iterating on Prompts

The prompts in `product/prompts/` are starting points. Customize them:

1. Add your team's specific requirements
2. Adjust output formats to match your tools
3. Include your quality standards
4. Add domain-specific guidance

Save customized versions and document changes.

---

## Expanding the System

This structure supports additional workflows:

### Potential Additions
- `product/roadmap/` - Roadmap planning documents
- `product/experiments/` - A/B test plans and results
- `product/analytics/` - User behavior analysis
- `product/releases/` - Release notes and planning
- `prompts/create-roadmap.md` - Roadmap generation from stories
- `prompts/analyze-user-behavior.md` - Analytics synthesis

### Integration Ideas
- Link to your issue tracker (Jira, Linear, etc.)
- Connect to design tools (Figma links in specs)
- Export stories to development tools
- Generate release notes from completed stories

---

## Getting Help

- **See available prompts**: `ls product/prompts/`
- **Read a prompt**: Ask to see any prompt file
- **Understand structure**: "Explain the directory structure"
- **Check status**: "What cycles do we have and which are complete?"

---

## Next Steps

1. ✅ Fill in `context/` files
2. ✅ Run `/cycle` to start your first discovery cycle
3. ✅ Conduct interview (or add additional interviews manually)
4. ✅ Run `/synth` to create synthesis
5. ✅ Run `/req` to extract epic and stories
6. ✅ Run `/jira` to load to backlog (optional)
7. ✅ Review timing data in `timing.json`
8. ✅ Repeat for next initiative!

---

**Remember**: This is an iterative system. Each cycle builds on previous learning!

In interactive mode, you can be conversational. Claude understands context and can help guide you through the workflows!
