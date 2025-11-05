# Claude PM - AI-Accelerated Product Discovery & Story Mapping

**Transform product discovery from weeks to hours** using AI-powered synthesis, story extraction, and visual story mapping.

## What is Claude PM?

Claude PM is a complete workflow for product managers using Claude Code and Miro to:
- Conduct structured stakeholder interviews
- Synthesize discovery findings with AI
- Extract user stories with complete acceptance criteria
- Create visual story maps in Miro
- Load stories directly to Jira

**Timeline**: From idea to development-ready backlog in 2-4 hours (vs 1-3 weeks traditional)

---

## Quick Start

### Prerequisites

1. **Claude Code** installed (https://docs.claude.com/claude-code)
2. **Atlassian MCP** configured for Jira access (optional, for Jira integration)
3. **Miro MCP** configured for story mapping (optional, for visual collaboration)
4. **Git** for version control

### Installation

1. Clone this repository to `~/dev/claudepm`
2. Open the directory in Claude Code
3. Tell Claude: "Please read the SETUP.md file and help me set up Claude PM for my project."

Claude will guide you through:
1. Filling in product context files
2. Understanding the workflow
3. Starting your first discovery cycle

---

## Directory Structure

```
claudepm/
├── README.md                          # This file
├── SETUP.md                           # First-time setup guide
├── .claude/
│   └── commands/                      # Slash commands
│       ├── cycle.md                   # Start new discovery cycle
│       ├── synth.md                   # Synthesize discovery
│       ├── req.md                     # Extract requirements
│       ├── map.md                     # Create story map
│       └── jira.md                    # Load to Jira
│
└── product/
    ├── README.md                      # Product workflow guide
    │
    ├── context/                       # Product knowledge base
    │   ├── product-overview.md
    │   ├── target-users.md
    │   ├── technical-context.md
    │   ├── competitive-landscape.md
    │   └── glossary.md
    │
    ├── discovery/                     # Research organized by cycles
    │   ├── interview-template.md
    │   ├── synthesis-template.md
    │   ├── YYYY-MM-DD-cycle-name/
    │   │   ├── README.md
    │   │   ├── interviews/
    │   │   ├── observations/
    │   │   └── synthesis-YYYY-MM-DD.md
    │   └── meta-synthesis/
    │
    ├── requirements/                  # User stories & epics
    │   ├── story-template.md
    │   ├── epic-template.md
    │   ├── stories-by-cycle.md        # Master index
    │   └── YYYY-MM-DD-cycle-name/
    │       ├── epic-###-name.md
    │       └── story-###-name.md
    │
    ├── story-maps/                    # Visual journey maps
    │   ├── README.md
    │   ├── BOARD-NAMING-CONVENTION.md
    │   ├── STORY-MAP-STRUCTURE.md
    │   ├── MIRO-CONVENTIONS.md
    │   └── YYYY-MM-DD-cycle-name/
    │       ├── story-map.md
    │       └── miro-metadata.json
    │
    └── prompts/                       # Reusable AI prompts
        ├── synthesize-discovery.md
        ├── extract-user-stories.md
        └── create-story-map.md
```

---

## The 4-Command Workflow

### 1. `/cycle` - Start Discovery Cycle

```
/cycle
```

**What it does**:
- Creates dated cycle directory
- Optionally conducts stakeholder interview
- Initializes README and tracking

**Output**: `product/discovery/YYYY-MM-DD-cycle-name/`

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
- Cross-references previous cycles

**Output**: `product/discovery/YYYY-MM-DD-cycle-name/synthesis-YYYY-MM-DD.md`

**Time**: 2-3 minutes

---

### 3. `/req` - Extract Requirements

```
/req
```

**What it does**:
- Converts synthesis into epic + stories
- Generates Given-When-Then acceptance criteria
- Includes non-functional requirements
- Updates stories-by-cycle index

**Output**:
- `product/requirements/YYYY-MM-DD-cycle-name/epic-###.md`
- `product/requirements/YYYY-MM-DD-cycle-name/story-###-*.md`

**Time**: 3-5 minutes

---

### 4. `/map` - Create Story Map (Optional)

```
/map
```

**What it does**:
- Creates visual user journey in Miro
- Organizes stories by activities
- Separates Now/Next/Later phases
- Enables team collaboration

**Output**:
- Miro board with story map
- `product/story-maps/YYYY-MM-DD-cycle-name/story-map.md`

**Time**: 2-3 minutes

---

### 5. `/jira` - Load to Backlog (Optional)

```
/jira
```

**What it does**:
- Creates epic in Jira
- Creates all stories with parent links
- Includes full acceptance criteria

**Output**: Jira tickets (e.g., SCRUM-40 through SCRUM-55)

**Time**: 1-2 minutes

---

## Example: End-to-End Flow

**Day 1 - Morning**:
```
9:00am  - /cycle → Interview stakeholder (15 min)
9:30am  - Add technical observations (30 min)
10:00am - /synth → AI creates synthesis (2 min)
10:15am - Review synthesis with team (15 min)
```

**Day 1 - Afternoon**:
```
1:00pm - /req → AI extracts epic + stories (3 min)
2:00pm - /map → Create visual story map (2 min)
2:15pm - Team grooming session in Miro (1 hour)
3:30pm - /jira → Load to backlog (1 min)
```

**Total**: ~3 hours from idea to ready backlog

---

## Key Features

### AI-Powered Synthesis
- Pattern recognition across interviews
- Consistent formatting at scale
- Evidence-based recommendations
- Cross-cycle learning

### Complete Acceptance Criteria
- Given-When-Then scenarios
- Non-functional requirements
- Quality checklists
- Technical notes
- Dependencies

### Visual Story Mapping
- User journey visualization
- Now/Next/Later planning
- Team collaboration in Miro
- Gap identification

### Full Traceability
- Interview → Synthesis → Story → Jira
- Git version control
- Stories-by-cycle index
- Change history

---

## Best Practices

### Context Management
- Keep `product/context/` files updated
- Update as product evolves
- AI uses these for every synthesis

### Discovery Cycles
- One focus per cycle (don't try to explore everything)
- 5-10 interviews recommended per cycle
- Include technical observations
- Run quarterly meta-synthesis

### Story Quality
- Review synthesis before extracting stories
- Run team grooming before Jira load
- Update stories as understanding evolves
- Document changes in story history

### Story Mapping
- Use when journeys are complex
- Enable personas only when needed
- Collaborate in Miro workshops
- Sync back to markdown before Jira load

---

## Requirements

### Required
- Claude Code
- Git

### Optional (Recommended)
- **Atlassian MCP** - For Jira integration
  - Direct story creation
  - Epic linking
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
A: Yes! Story mapping is optional. You can skip `/map` and go straight from `/req` to `/jira`.

**Q: How do I customize the workflow?**
A: Edit files in `product/prompts/` to change AI behavior, or edit slash commands in `.claude/commands/`.

**Q: Can I use this for non-software products?**
A: Yes! Adjust templates and context files for your domain.

**Q: What if I have multiple products?**
A: Create separate directories or use branches in git.

---

## Customization

### Templates
Edit these to match your team's format:
- `product/discovery/interview-template.md`
- `product/discovery/synthesis-template.md`
- `product/requirements/story-template.md`
- `product/requirements/epic-template.md`

### Prompts
Modify AI behavior:
- `product/prompts/synthesize-discovery.md`
- `product/prompts/extract-user-stories.md`
- `product/prompts/create-story-map.md`

### Slash Commands
Add your own commands in `.claude/commands/`:
- Create new workflows
- Add custom validations
- Integrate with other tools

---

## Examples

See the `examples/` directory for:
- Complete discovery cycle (Authentication)
- Synthesis document
- Epic and stories
- Story map
- Jira tickets

---

## Troubleshooting

### Slash commands not working
**Solution**: Commands are in `.claude/commands/`. Check they're installed correctly.

### AI synthesis is too generic
**Solution**: Fill in `product/context/` files with more specific product details.

### Stories missing acceptance criteria
**Solution**: Review `product/requirements/story-template.md` to ensure format is correct.

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

Open the `claudepm` directory in Claude Code and tell Claude: "Help me set up my first discovery cycle"
