# Claude PM - First-Time Setup Guide

Welcome to Claude PM! This guide will help you set up your first AI-accelerated product discovery workflow.

---

## Prerequisites

Before starting, ensure you have:

1. **Claude Code** installed
   - Download from https://docs.claude.com/claude-code
   - Verify installation: `claude-code --version`

2. **Git** for version control
   - Verify: `git --version`

3. **Atlassian MCP** (optional, for Jira integration)
   - Follow setup at https://github.com/modelcontextprotocol/servers/tree/main/src/atlassian

4. **Miro MCP** (optional, for story mapping)
   - Follow setup at https://github.com/modelcontextprotocol/servers/tree/main/src/miro

---

## Step 1: Clone or Copy This Repository

```bash
# If you're starting from GitHub:
cd ~/dev
git clone https://github.com/YOUR-ORG/claudepm.git my-product
cd my-product

# OR if you downloaded as ZIP:
cd ~/dev/my-product
```

---

## Step 2: Fill In Product Context

The `product/context/` directory contains templates that Claude uses to understand your product. Fill these in before your first iteration.

### 2.1 Product Overview (`product/context/product-overview.md`)

**What to include:**
- Product name and tagline
- Core value proposition
- Key features (high-level)
- Business model (if applicable)
- Current stage (ideation, MVP, growth, etc.)

**Example:**
```markdown
# Product: TaskFlow Pro

**Tagline**: Smart task management for distributed teams

**Value Proposition**:
Helps remote teams coordinate complex projects with AI-powered
task breakdown and intelligent scheduling.

**Current Stage**: MVP - 50 beta users
```

**Time to complete**: 10-15 minutes

---

### 2.2 Target Users (`product/context/target-users.md`)

**What to include:**
- Primary user personas (2-4 personas)
- User goals and pain points
- Usage patterns
- Demographics (if relevant)

**Example:**
```markdown
# Primary Personas

## Remote Team Lead
- **Goals**: Coordinate team of 5-10 people across time zones
- **Pains**: Losing track of who's working on what
- **Frequency**: Daily user, 2-3 hours per day

## Individual Contributor
- **Goals**: Stay focused, avoid context switching
- **Pains**: Too many tools, unclear priorities
- **Frequency**: Daily user, 30 min per day
```

**Time to complete**: 15-20 minutes

---

### 2.3 Technical Context (`product/context/technical-context.md`)

**What to include:**
- Tech stack (frontend, backend, infrastructure)
- Constraints (performance, security, compliance)
- Integrations (third-party services)
- Architecture decisions already made

**Example:**
```markdown
# Tech Stack

**Frontend**: React, TypeScript, Tailwind CSS
**Backend**: Node.js, Express, PostgreSQL
**Infrastructure**: GCP (Cloud Run, Cloud SQL)
**Integrations**: Slack, Google Calendar, GitHub

# Constraints
- Must support GDPR compliance
- Max page load: 2 seconds
- Mobile-responsive (iOS, Android browsers)
```

**Time to complete**: 10-15 minutes

---

### 2.4 Competitive Landscape (`product/context/competitive-landscape.md`)

**What to include:**
- Direct competitors (2-5)
- Indirect competitors or alternatives
- Your differentiation
- Market trends

**Example:**
```markdown
# Direct Competitors

## Asana
- **Strengths**: Established, feature-rich
- **Weaknesses**: Complex UI, steep learning curve
- **Our Differentiation**: AI task breakdown, simpler UX

## Linear
- **Strengths**: Fast, developer-focused
- **Weaknesses**: Limited PM features
- **Our Differentiation**: Better for non-technical teams
```

**Time to complete**: 10 minutes

---

### 2.5 Glossary (`product/context/glossary.md`)

**What to include:**
- Domain-specific terms
- Acronyms used in your product
- Technical jargon that needs definition

**Example:**
```markdown
# Glossary

**Workspace**: A team's container for all projects and tasks
**Sprint**: 2-week iteration cycle
**Epic**: Large feature spanning multiple sprints
**Story Points**: Relative effort estimation (1, 2, 3, 5, 8, 13)
```

**Time to complete**: 5-10 minutes

---

## Step 3: Start Claude Code

```bash
cd ~/dev/my-product
claude-code
```

**First message to Claude:**
```
Please read the SETUP.md file and help me verify my context files are complete.
```

Claude will:
- Review your context files
- Suggest improvements or missing information
- Confirm you're ready for your first iteration

---

## Step 4: Run Your First Iteration

### Option A: With Stakeholder Interview

```
/iter
```

Claude will:
1. Create an iteration directory (e.g., `product/iterations/2025-11-mvp/`)
2. Optionally conduct a structured interview with stakeholder
3. Document interview notes
4. Set up tracking files

**Time**: 15-30 minutes

---

### Option B: Add Research Manually

```
/iter
```

Then decline the interview and add your own research:
- Interview notes
- User feedback
- Analytics insights
- Support ticket analysis
- Competitive research

Add files to: `product/iterations/[ITERATION]/discovery/`

**Time**: 30-60 minutes (depending on research)

---

## Step 5: Run Synthesis

After collecting discovery materials:

```
/synth
```

Claude will:
- Analyze all materials in the current iteration
- Identify 4-6 themes
- Propose 8-12 features
- Cross-reference previous iterations
- Generate synthesis document

**Output**: `product/iterations/[ITERATION]/discovery/synthesis/synthesis-YYYY-MM-DD.md`

**Time**: 2-3 minutes

---

## Step 6: Extract User Stories

After reviewing synthesis:

```
/req
```

Claude will:
- Convert synthesis into user stories
- Generate Given-When-Then acceptance criteria
- Include non-functional requirements
- Create stories index

**Output**:
- `product/iterations/[ITERATION]/stories/story-###-*.md`
- `product/iterations/[ITERATION]/stories/stories-index.md`

**Time**: 3-5 minutes

---

## Step 7: Create Story Map (Optional)

If you want to visualize the user journey:

### 7.1 Create Miro Board Manually

**Important**: Miro boards cannot be created via API

1. Go to https://miro.com
2. Create new board
3. Name it: `Story Map - [Iteration Name]`
4. Copy the board ID from URL

### 7.2 Generate Story Map

```
/map
```

Claude will:
- Prompt for Miro board selection
- Ask if personas should be included
- Create visual story map in Miro
- Generate markdown documentation

**Output**:
- Miro board with story map
- `product/iterations/[ITERATION]/story-maps/story-map.md`

**Time**: 2-3 minutes

---

## Step 8: Sync Priorities from Miro (Optional)

After team grooming in Miro:

```
/demap
```

Claude will:
- Read priorities from Miro board
- Update story markdown files with new priorities
- Handle new stories added in Miro
- Flag stories removed from map

**Time**: 1-2 minutes

---

## Step 9: Load to Jira (Optional)

If you have Atlassian MCP configured:

```
/jira
```

Claude will:
- Create stories in Jira
- Include full acceptance criteria
- Apply appropriate labels

**Output**: Jira tickets (e.g., PROJ-100 through PROJ-115)

**Time**: 1-2 minutes

---

## Step 10: Reconcile Releases (Optional)

After development is complete:

```
/rel
```

Claude will:
- Process release notes
- Update story statuses to "Built"
- Update product specification

**Time**: 2-3 minutes

---

## Complete First Iteration Timeline

**Minimal path** (no Miro, no Jira):
```
15-30 min - /iter (with interview)
2-3 min  - /synth
3-5 min  - /req
Total: ~25-40 minutes to development-ready stories
```

**Full path** (with Miro and Jira):
```
15-30 min - /iter
2-3 min  - /synth
3-5 min  - /req
2-3 min  - /map (create visual story map)
15-60 min - Team grooming session in Miro
1-2 min  - /demap (sync priorities back)
1-2 min  - /jira
Total: ~40-105 minutes to stories in backlog
```

---

## Troubleshooting

### Slash commands not working

**Symptom**: `/iter` returns "command not found"

**Solution**:
- Commands are in `.claude/commands/`
- Ensure Claude Code is running in your project directory
- Check that `.claude/commands/*.md` files exist

---

### AI synthesis is too generic

**Symptom**: Synthesis doesn't capture product nuances

**Solution**:
- Fill in more detail in `product/context/` files
- Add more specific user quotes in interviews
- Include concrete examples in discovery materials

---

### Stories missing acceptance criteria

**Symptom**: Stories have vague requirements

**Solution**:
- Review story templates in `product/templates/`
- Ensure synthesis has enough detail
- Add technical notes to discovery materials

---

### Miro board creation fails

**Symptom**: "Cannot create board" error

**Solution**:
- Boards must be created manually in Miro web UI
- Claude can only add items to existing boards
- See Step 7.1 for manual board creation

---

### Jira integration not working

**Symptom**: Cannot create tickets in Jira

**Solution**:
- Verify Atlassian MCP is configured
- Check cloud ID is correct
- Ensure you have create permission in target project
- Run `mcp__atlassian__getVisibleJiraProjects` to verify access

---

## Next Steps

After completing your first iteration:

1. **Review the output**
   - Read synthesis document
   - Review generated stories
   - Check story map visualization (if created)

2. **Run team grooming**
   - Share story map with team
   - Discuss priorities
   - Identify gaps

3. **Start development**
   - Load stories to Jira
   - Begin sprint planning
   - Track progress

4. **Plan next iteration**
   - What to explore next?
   - Which user problems remain?
   - What technical decisions need research?

---

## Tips for Success

### Context is King
- Keep `product/context/` files updated as product evolves
- Claude references these for every synthesis
- More detail = better synthesis

### One Focus Per Iteration
- Don't try to explore everything at once
- 5-10 interviews per iteration is ideal
- Deep beats broad

### Include Technical Observations
- Developers should add technical notes
- Capture architecture decisions
- Document constraints discovered

### Regular Meta-Synthesis
- Run periodic meta-synthesis across all iterations
- Identify long-term patterns
- Update product strategy

### Story Quality Over Speed
- Review synthesis before extracting stories
- Run team grooming before Jira load
- Update stories as understanding evolves

---

## Key Concepts

### Iterations (Not Sprints)
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
- Stories are numbered sequentially across ALL iterations (never reset)
- STORY-001, STORY-002, ... STORY-044 → next iteration continues at STORY-045

---

## Example Workflow

**Monday Morning:**
```
9:00am  - /iter → Interview product manager (15 min)
9:30am  - Add engineering notes from tech spike (30 min)
10:00am - /synth → AI creates synthesis (2 min)
10:15am - Review synthesis with team (15 min)
```

**Monday Afternoon:**
```
1:00pm - /req → AI extracts stories (3 min)
2:00pm - /map → Create visual story map (2 min)
2:15pm - Team grooming in Miro (1 hour)
3:15pm - /demap → Sync priorities back (1 min)
3:30pm - /jira → Load to backlog (1 min)
```

**Total**: ~3 hours from idea to ready backlog

**Traditional approach**: 1-3 weeks

---

## Getting Help

**Documentation**:
- `README.md` - Main project documentation
- `product/README.md` - Detailed workflow guide
- `CLAUDE.md` - AI context and architecture

**Ask Claude**:
```
How do I customize the synthesis prompt?
What's the difference between /iter and /synth?
Can you show me an example story file?
```

**Community**:
- Issues: https://github.com/YOUR-ORG/claudepm/issues
- Discussions: https://github.com/YOUR-ORG/claudepm/discussions

---

## Ready to Start?

```bash
cd ~/dev/my-product
claude-code
```

Then:
```
Let's start my first iteration on [your topic]
```

Claude will guide you through the rest!
