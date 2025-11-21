# Claude PM - AI-Accelerated Product Discovery & Story Mapping

**Transform product discovery from weeks to hours** using AI-powered synthesis, story extraction, and visual story mapping.

## What is Claude PM?

Claude PM is a complete workflow for product managers using Claude Code and Miro to:
- Conduct structured stakeholder interviews
- Synthesize discovery findings with AI
- Extract user stories with complete acceptance criteria
- Create visual story maps in Miro
- Sync priorities from team collaboration
- Load stories directly to Jira
- Reconcile releases and update product specifications

**Timeline**: From idea to development-ready backlog in 2-4 hours (vs 1-3 weeks traditional)

---

## Quick Start

### Prerequisites

1. **Claude Code** installed (https://docs.anthropic.com/claude-code)
2. **Atlassian MCP** configured for Jira access (optional, for Jira integration)
3. **Miro MCP** configured for story mapping (optional, for visual collaboration)
4. **Git** for version control

### Installation

1. Clone this repository to your project directory
2. Copy the product directory to your repository:
   ```bash
   cp -r claudepm/product ./product
   ```
3. Copy the slash commands to your repository root:
   ```bash
   mkdir -p .claude/commands
   cp claudepm/.claude/commands/* .claude/commands/
   ```
4. Open your repository in Claude Code
5. Run `/setup` to populate product context through an interactive interview
   - Or manually edit files in `product/context/` if you prefer
   - Or skip setup and start with `/iter` to dive right in

The `/setup` command offers three depth levels:
- **Quick Start** (5-10 min): Product overview only
- **Standard** (15-20 min): Product overview + target users
- **Complete** (30-40 min): All context including competitive landscape and tech stack

---

## Directory Structure

```
claudepm/
├── README.md                          # This file
├── SETUP.md                           # First-time setup guide
│
├── .claude/commands/                  # Slash commands
│   ├── setup.md                       # Initial product context interview
│   ├── iter.md                        # Start new iteration
│   ├── synth.md                       # Synthesize discovery
│   ├── req.md                         # Extract requirements
│   ├── map.md                         # Create Miro story map
│   ├── demap.md                       # Sync Miro priorities back
│   ├── jira.md                        # Load to Jira
│   └── recon.md                       # Reconcile releases
│
└── product/
    ├── README.md                      # Product workflow guide
    │
    ├── iterations/                    # All iteration artifacts
    │   └── YYYY-MM-name/              # Example: 2025-11-mvp
    │       ├── discovery/
    │       │   ├── interviews/
    │       │   ├── observations/
    │       │   ├── synthesis/
    │       │   └── README.md
    │       ├── stories/
    │       │   ├── story-001-*.md
    │       │   └── archive/
    │       ├── story-maps/
    │       │   ├── miro-metadata.json
    │       │   └── story-map.md
    │       ├── design/
    │       │   └── screenshots/
    │       ├── releases/
    │       │   └── release-001-*.md
    │       └── timing.json
    │
    ├── backlog.md                     # Ready stories not yet built
    ├── product-spec.md                # Current product capabilities
    │
    ├── context/                       # Product knowledge base
    │   ├── product-overview.md
    │   ├── target-users.md
    │   ├── technical-context.md
    │   ├── competitive-landscape.md
    │   └── glossary.md
    │
    ├── templates/                     # Reusable templates
    │   ├── story-template-llm-dev.md
    │   ├── story-template-human-dev.md
    │   ├── interview-template.md
    │   ├── synthesis-template.md
    │   ├── product-spec-template.md
    │   └── rule-template.md
    │
    ├── prompts/                       # Reusable AI prompts
    │   ├── synthesize-discovery.md
    │   ├── extract-user-stories.md
    │   ├── create-story-map.md
    │   ├── load-stories-to-tracker.md
    │   └── reconcile-and-update-spec.md
    │
    ├── rules/                         # LLM prompting rules
    │   └── README.md
    │
    └── artifacts/                     # Generated outputs
        └── timing-log.jsonl
```

---

## The Workflow

### 0. `/setup` - Initial Product Context (Optional)

```
/setup
```

**What it does**:
- Interactive interview to populate product context
- Three depth levels: Quick Start, Standard, Complete
- Creates files in `product/context/`

**Output**: `product/context/*.md` files with your product information

**Time**: 5-40 minutes (depending on depth level chosen)

---

### 1. `/iter` - Start Iteration

```
/iter
```

**What it does**:
- Creates iteration directory structure
- Optionally conducts stakeholder interview
- Initializes README and tracking
- Records timing metrics

**Output**: `product/iterations/YYYY-MM-name/`

**Time**: 15-30 minutes (with interview)

---

### 2. `/synth` - Synthesize Findings

```
/synth
```

**What it does**:
- AI analyzes all discovery materials
- Identifies 4-6 themes
- Proposes 8-12 features
- Cross-references previous iterations

**Output**: `product/iterations/{iteration}/discovery/synthesis/synthesis-{date}.md`

**Time**: 2-3 minutes

---

### 3. `/req` - Extract Requirements

```
/req
```

**What it does**:
- Converts synthesis into user stories
- Generates Given-When-Then acceptance criteria
- Includes non-functional requirements
- Sequential numbering across all iterations

**Output**: `product/iterations/{iteration}/stories/story-###-*.md`

**Time**: 3-5 minutes

---

### 4. `/map` - Create Story Map (Optional)

```
/map
```

**What it does**:
- Creates visual user journey in Miro
- Organizes stories by activities
- Creates NOW/NEXT/LATER swim lanes
- Enables team collaboration

**Output**:
- Miro board with story map
- `product/iterations/{iteration}/story-maps/miro-metadata.json`

**Time**: 2-3 minutes

---

### 5. `/demap` - Sync Priorities (Optional)

```
/demap
```

**What it does**:
- Reads current Miro board state
- Updates story priorities based on swim lane positions
- Handles new stories added to Miro
- Archives stories removed from Miro

**Output**: Updated story files with latest priorities

**Time**: 1-2 minutes

---

### 6. `/jira` - Load to Backlog (Optional)

```
/jira
```

**What it does**:
- Creates stories in Jira
- Includes full acceptance criteria
- Uses labels to group iteration stories

**Output**: Jira tickets (e.g., PROJ-40 through PROJ-55)

**Time**: 1-2 minutes

---

### 7. `/recon` - Reconcile Release (Optional)

```
/recon
```

**What it does**:
- Parses release notes for story IDs
- Updates story statuses: Ready → Built
- Creates release artifact
- Updates Product Specification

**Output**:
- Updated story files
- Release artifact in `iterations/{iteration}/releases/`
- Updated `product-spec.md`

**Time**: 2-3 minutes

---

## Example: End-to-End Flow

**Day 1 - Morning**:
```
9:00am  - /iter → Interview stakeholder (15 min)
9:30am  - Add technical observations (30 min)
10:00am - /synth → AI creates synthesis (2 min)
10:15am - Review synthesis with team (15 min)
```

**Day 1 - Afternoon**:
```
1:00pm - /req → AI extracts stories (3 min)
2:00pm - /map → Create visual story map (2 min)
2:15pm - Team grooming session in Miro (1 hour)
3:15pm - /demap → Sync priorities from Miro (1 min)
3:30pm - /jira → Load to backlog (1 min)
```

**After Release**:
```
/recon → Update statuses, create release artifact, update product spec
```

**Total**: ~3 hours from idea to ready backlog

---

## Key Concepts

### Iterations vs Sprints

**Iterations are NOT time-boxed sprints**. They are:
- **Arbitrary length** - Could be days, weeks, or months
- **Initiative-focused** - Bound to a feature area or business goal
- **Concurrent** - Multiple iterations can be active simultaneously
- **Context containers** - Keep LLM context manageable by limiting scope

### Story Lifecycle

```
Draft → Ready → Built
         ↓
      Backlog (if not built in iteration)
         ↓
      Archived (if removed from scope)
```

### Story Numbering

Stories are numbered sequentially across ALL iterations (never reset):
- STORY-001, STORY-002, ... STORY-044
- New iteration continues from highest number

---

## Key Features

### AI-Powered Synthesis
- Pattern recognition across interviews
- Consistent formatting at scale
- Evidence-based recommendations
- Cross-iteration learning

### Complete Acceptance Criteria
- Given-When-Then scenarios
- Non-functional requirements
- Quality checklists
- Technical notes
- Dependencies

### Visual Story Mapping
- User journey visualization
- NOW/NEXT/LATER planning
- Team collaboration in Miro
- Bidirectional sync with `/map` and `/demap`

### Full Traceability
- Interview → Synthesis → Story → Jira
- Git version control
- Release reconciliation
- Product specification updates

### Timing Metrics
- Per-iteration timing in `timing.json`
- Global timing log in `artifacts/timing-log.jsonl`
- Track workflow efficiency over time

---

## Requirements

### Required
- Claude Code
- Git

### Optional (Recommended)
- **Atlassian MCP** - For Jira integration
  - Direct story creation
  - No copy-paste errors

- **Miro MCP** - For story mapping
  - Visual collaboration
  - Journey visualization
  - Team workshops

---

## FAQ

**Q: Can I use this without Jira?**
A: Yes! Stories are created as markdown files. You can manually create Jira tickets or use any other tracker.

**Q: Can I use this without Miro?**
A: Yes! Story mapping is optional. You can skip `/map` and `/demap` and go straight from `/req` to `/jira`.

**Q: How do I customize the workflow?**
A: Edit files in `product/prompts/` to change AI behavior, or edit slash commands in `.claude/commands/`.

**Q: Can I use this for non-software products?**
A: Yes! Adjust templates and context files for your domain.

**Q: What if I have multiple products?**
A: Create separate directories or use branches in git.

**Q: What's the difference between `/map` and `/demap`?**
A: `/map` creates the Miro board from stories (markdown → Miro). `/demap` syncs changes back (Miro → markdown).

---

## Customization

### Templates
Edit these to match your team's format:
- `product/templates/story-template-llm-dev.md` - For LLM-centric development
- `product/templates/story-template-human-dev.md` - For human-centric development
- `product/templates/interview-template.md`
- `product/templates/synthesis-template.md`

### Prompts
Modify AI behavior:
- `product/prompts/synthesize-discovery.md`
- `product/prompts/extract-user-stories.md`
- `product/prompts/create-story-map.md`
- `product/prompts/reconcile-and-update-spec.md`

### Slash Commands
Modify commands in `.claude/commands/`:
- Create new workflows
- Add custom validations
- Integrate with other tools

---

## Troubleshooting

### Slash commands not working
**Solution**: Make sure you copied the commands to `.claude/commands/` at your repository root.

### AI synthesis is too generic
**Solution**: Fill in `product/context/` files with more specific product details.

### Stories missing acceptance criteria
**Solution**: Review the story templates in `product/templates/` to ensure format is correct.

### Miro board creation fails
**Solution**: Boards must be manually created in Miro web UI. Claude cannot create boards via API.

---

## Support

- **Documentation**: See `product/README.md` for detailed workflow guide
- **Issues**: https://github.com/trigrman/claudepm/issues
- **Discussions**: https://github.com/trigrman/claudepm/discussions

---

## Credits

Built with:
- **Claude Code** by Anthropic
- **Atlassian MCP** for Jira integration
- **Miro MCP** for story mapping
- Inspired by Jeff Patton's "User Story Mapping"

---

**Ready to transform your product discovery?**

Open your project directory in Claude Code and run `/iter` to start your first iteration!
