# Miro Story Map Conventions

## Overview

These conventions ensure consistency across all story maps and enable reliable Miro↔Markdown sync.

---

## Before Creating a Map

**Ask the user**: "Include user personas on this map? (y/n)"

- **Yes**: Add persona emojis to cards + create legend
- **No**: Skip emojis (infrastructure already color-coded)

**When to use personas**:
- Multiple user types with different journeys
- Journeys that transition between personas
- Need to distinguish who does what

**When to skip personas**:
- Single user type
- All stories apply to same persona
- Infrastructure-only initiatives

---

## Structure

### Horizontal Axis (Left to Right)
**User's journey through time** - activities in chronological order

Example: Setup → Sign Up → Log In → Use App → Manage Account → Recover Access

### Vertical Axis (Top to Bottom)
**Priority within each activity**

1. Backbone (activity headers) at top
2. Stories below, most essential first
3. Horizontal separator bars divide phases

### Phase Separators

**Gray bars with white text** spanning the width:

```
─────────── Stories above this line ───────────
─────────── NOW (Walking Skeleton) ─────────────
─────────── Stories between NOW and NEXT ───────
─────────── NEXT ─────────────
─────────── Stories between NEXT and LATER ─────
─────────── LATER ─────────────
─────────── Stories below (future/deferred) ────
```

**Why gray**: Doesn't compete with card colors (which indicate type)

---

## Color Coding (By Type, Not Phase)

### Card Colors

| Color | Type | When to Use |
|-------|------|-------------|
| **Blue** | Activity headers (backbone) | Major steps in user journey |
| **Yellow** | User stories | All user-facing functionality |
| **Violet** | Spikes/Research | Technical decisions, unknowns |
| **Cyan** | Infrastructure | Backend, DevOps, database, etc. |
| **Red** | Risks | Identified risks or blockers |
| **Orange** | Questions | Open questions, assumptions |
| **Gray** | Pains/Challenges | User pain points, problems |

**Important**: Color indicates **type**, not priority or phase
- Stories move between NOW/NEXT/LATER during collaboration
- Color stays the same (a user story is always yellow)

---

## Persona Emojis

**When personas are enabled**, prefix story cards with emoji:

| Emoji | Persona | Description |
|-------|---------|-------------|
| ⚙️ | Developer | Infrastructure, DevOps, technical setup |
| 👤 | New User | First-time user, sign up, onboarding |
| 🔁 | Returning User | Existing user, repeat usage |
| 👥 | All Users | Applies to everyone (can be omitted) |
| 🛒 | Shopper | (Custom - e.g., e-commerce) |
| 📊 | Admin | (Custom - admin functionality) |

**Rules**:
- Add emoji prefix to card content: "⚙️ STORY-001"
- Only use when it matters (if most cards are one persona, only mark exceptions)
- Create legend on the board showing all personas used

**Converting to .md**:
- Emoji → Text in story metadata: "⚙️" becomes `Persona: Developer`
- If no emoji, defaults to primary persona or "All Users"

---

## Card Format

### Backbone (Activity Headers)
```
Activity Name
(no story ID, just the activity)
```

**Color**: Blue
**Font**: Larger (Miro auto-sizing)
**Example**: "Sign Up", "Log In", "Use App"

### User Stories
```
[Persona] STORY-###
Story Name
Brief description
```

**Color**: Yellow
**Font**: Miro auto-sizing
**Example**:
```
👤 STORY-005
User Registration
Backend API
```

### Infrastructure Stories
```
⚙️ STORY-###
Story Name
Brief description
```

**Color**: Cyan
**Font**: Miro auto-sizing

### Spikes
```
⚙️ SPIKE-###
Spike Name
Brief description
Time-box | Blocking/Non-blocking
```

**Color**: Violet
**Font**: Miro auto-sizing
**Example**:
```
⚙️ SPIKE-001
Compute Platform
4h | Blocking
```

### Other Types (Risks, Questions, Pains)
```
[Icon/Emoji] Description
Additional context
```

**Examples**:
- **Risk**: "⚠️ Third-party API reliability unknown"
- **Question**: "❓ Do users need mobile app access?"
- **Pain**: "😞 Users forget passwords frequently"

---

## Spacing

### Horizontal (Between Activities)
**500px** between activity columns

**Coordinates for typical 6-activity map**:
- Activity 1: x = -1400
- Activity 2: x = -900
- Activity 3: x = -400
- Activity 4: x = 100
- Activity 5: x = 600
- Activity 6: x = 1100

### Vertical (Between Cards)
**200px** between cards in same column

**Coordinates**:
- Backbone: y = -1000
- First story: y = -800
- Second story: y = -600
- Third story: y = -400
- Fourth story: y = -200
- Fifth story: y = 0
- Sixth story: y = 200

**Separator bars**:
- NOW bar: y = 400 (below last NOW story)
- NEXT bar: y = 800 (below last NEXT story)
- LATER bar: y = 1200 (below last LATER story)

---

## Legend (When Using Personas)

Place legend in top-right corner:

```
┌─────────────────────┐
│ PERSONAS            │
├─────────────────────┤
│ ⚙️  Developer        │
│ 👤 New User         │
│ 🔁 Returning User   │
└─────────────────────┘
```

**Position**: x = 1400, y = -1000
**Color**: Light gray
**Font**: Small

---

## Board Layout Example

```
                    [LEGEND]

⚙️ Setup      Sign Up     Log In      Use App     Manage      Recover
Infrastructure                                    Account     Access
──────────────────────────────────────────────────────────────────────
⚙️ SPIKE-001   👤 STORY-012  STORY-006   STORY-010  STORY-009   STORY-007
⚙️ SPIKE-002   👤 STORY-005  STORY-011
⚙️ STORY-001
⚙️ STORY-002
⚙️ STORY-003
⚙️ STORY-004

──────────────────── NOW (Walking Skeleton) ────────────────────────

              👤 STORY-013  🔁 STORY-008

──────────────────── NEXT ──────────────────────────────────────────

              [future stories]

──────────────────── LATER ─────────────────────────────────────────

              [deferred stories]
```

---

## Miro→Markdown Parsing Rules

### Identifying Phases
- **NOW**: Stories with y-coordinate < NOW bar y-position
- **NEXT**: Stories between NOW bar and NEXT bar
- **LATER**: Stories between NEXT bar and LATER bar
- **Future**: Stories below LATER bar

### Extracting Persona
- Parse emoji prefix from card content
- Map emoji to persona name
- If no emoji, use default persona or "All Users"

### Extracting Story ID
- Parse "STORY-###" or "SPIKE-###" from card content
- Link to existing .md file in requirements/ directory

### Determining Activity
- Find which backbone activity card is closest horizontally
- Group story under that activity

---

## Creating a New Story Map

### Workflow

1. **Prompt for personas**: "Include user personas? (y/n)"
2. **Create Miro board manually**: User creates board in Miro web UI
3. **Get board ID**: List boards, find the new one
4. **Identify activities**: Analyze user journey, extract 4-8 major steps
5. **Create backbone**: Blue cards for activities, left to right
6. **Add stories**:
   - Group under appropriate activity
   - Add persona emoji if enabled
   - Color by type (yellow=user, cyan=infra, violet=spike)
   - Use proper spacing
7. **Add separator bars**: Gray bars for NOW/NEXT/LATER
8. **Add legend**: If personas enabled, show emoji mappings
9. **Create .md snapshot**: Document the map in markdown

---

## Best Practices

### Do
✅ Use consistent spacing (500px horizontal, 200px vertical)
✅ Color by type (yellow=user stories, cyan=infrastructure)
✅ Only use personas when they add clarity
✅ Keep backbone to 4-8 activities
✅ Use gray separator bars (not colors that compete with cards)
✅ Create legend when using personas
✅ Let Miro auto-size fonts

### Don't
❌ Don't use color to indicate phase (use separator bars)
❌ Don't add too many activities (keep it simple)
❌ Don't use personas if there's only one user type
❌ Don't let cards overlap (maintain spacing)
❌ Don't use different font sizes manually (let Miro handle it)
❌ Don't forget to add LATER bar (users need somewhere to put future ideas)

---

## Troubleshooting

### Cards overlap
**Problem**: Not enough spacing
**Solution**: Use 500px horizontal, 200px vertical

### Can't tell phases apart
**Problem**: Stories not clearly separated
**Solution**: Ensure gray separator bars are visible and labeled

### Confusing persona usage
**Problem**: Too many emojis or unclear which persona is which
**Solution**: Only use personas when needed, create clear legend

### Sync issues
**Problem**: Changes in Miro don't reflect in .md files
**Solution**: Run `/map` sync after workshop changes

---

## Example Use Cases

### Simple Initiative (No Personas)
**Scenario**: Adding search functionality
**Personas**: No (all users use search)
**Activities**: Enter Query → View Results → Filter → Select Item
**Card colors**: Yellow (user stories), Cyan (infrastructure), Violet (spikes)

### Complex Initiative (With Personas)
**Scenario**: Multi-user e-commerce checkout
**Personas**: Yes (Guest, Registered User, Admin)
**Activities**: Browse → Add to Cart → Checkout → Pay → Track Order
**Legend**: 👤 Guest, 🔁 Registered User, 📊 Admin

### Infrastructure-Heavy (Minimal Personas)
**Scenario**: Database migration
**Personas**: No (all DevOps work)
**Activities**: Plan → Backup → Migrate → Verify → Rollback Plan
**Card colors**: Mostly Cyan (infrastructure), some Violet (spikes)

---

## Integration with `/map` Command

The `/map` slash command will:

1. Prompt: "Include user personas? (y/n)"
2. Detect/create Miro board
3. Parse stories or synthesis
4. Generate story map following these conventions
5. Create legend if personas enabled
6. Add separator bars (NOW/NEXT/LATER)
7. Apply proper spacing and colors
8. Create markdown snapshot

**Sync direction**:
- **Stories→Miro**: Read .md files, create/update Miro board
- **Miro→Markdown**: Read Miro board, create/update .md files
