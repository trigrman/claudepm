# Story Map Structure Rules

Based on Jeff Patton's User Story Mapping methodology.

## Core Principles

### Horizontal Axis (Left to Right)
**Represents**: User's journey through time - the sequence of activities

**Flow**: What the user does first → second → third → etc.

**Example**: Discover → Sign Up → Log In → Use App → Manage Account

### Vertical Axis (Top to Bottom)
**Represents**: Priority and necessity

**Order**:
1. **Top**: Backbone (activity headers - blue cards)
2. **Below**: Must Have stories (essential for walking skeleton)
3. **Further down**: Should Have stories (nice to have)
4. **Bottom**: Could Have stories (future enhancements)

---

## Story Map Anatomy

```
┌─────────────────────────────────────────────────────────────┐
│                    EPIC HEADER (optional)                    │
└─────────────────────────────────────────────────────────────┘

BACKBONE (Blue cards - Activities in chronological order):
┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐
│Activity│  │Activity│  │Activity│  │Activity│  │Activity│
│   1    │  │   2    │  │   3    │  │   4    │  │   5    │
└────────┘  └────────┘  └────────┘  └────────┘  └────────┘
    │            │            │            │            │
    ▼            ▼            ▼            ▼            ▼
┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐
│ Story  │  │ Story  │  │ Story  │  │ Story  │  │ Story  │
│  Must  │  │  Must  │  │  Must  │  │  Must  │  │  Must  │
└────────┘  └────────┘  └────────┘  └────────┘  └────────┘
┌────────┐  ┌────────┐  ┌────────┐
│ Story  │  │ Story  │  │ Story  │
│  Must  │  │  Must  │  │  Must  │
└────────┘  └────────┘  └────────┘

───────────── NOW (Walking Skeleton) ─────────────

┌────────┐  ┌────────┐  ┌────────┐
│ Story  │  │ Story  │  │ Story  │
│ Should │  │ Should │  │ Should │
└────────┘  └────────┘  └────────┘

───────────── LATER ─────────────

┌────────┐  ┌────────┐
│ Story  │  │ Story  │
│ Could  │  │ Could  │
└────────┘  └────────┘
```

---

## Spacing Guidelines

**Horizontal spacing** (between activity columns):
- 400px between activity columns
- Ensures cards don't overlap and map is readable

**Vertical spacing** (between cards in same column):
- 170px between cards
- Allows room for card content without crowding

**Coordinates for 6-activity map**:
- Activity 1: x = -1200
- Activity 2: x = -800
- Activity 3: x = -400
- Activity 4: x = 0
- Activity 5: x = 400
- Activity 6: x = 800

**Vertical positions**:
- Backbone: y = -900
- First story: y = -700
- Second story: y = -530
- Third story: y = -360
- Fourth story: y = -190
- Fifth story: y = -20
- Etc...

---

## Color Coding

**Backbone (Activities)**: Blue
- Represents major user activities/steps

**Must Have**: Yellow
- Essential for minimal viable journey (walking skeleton)

**Should Have**: Light Green
- Important but not critical for first release

**Could Have**: Light Pink
- Nice to have enhancements

**Spikes/Research**: Violet
- Technical decisions needed before implementation

**Infrastructure**: Cyan (optional)
- Can be shown separately or integrated into flow

---

## Now/Next/Later (Optional)

Use horizontal divider lines when stories warrant phasing:

**NOW (Walking Skeleton)**:
- All Must Have stories above this line
- Minimal viable user journey
- Usually maps to first release/sprint

**LATER**:
- Should Have and Could Have stories below
- Enhancements and polish
- Future iterations

**Don't use** if there aren't enough stories to warrant separation (< 10 stories total)

---

## Building a Story Map

### Step 1: Identify Activities (Backbone)
Ask: "What are the major steps in the user's journey?"
- Start with verb phrases (Discover, Sign Up, Log In, etc.)
- Order chronologically left to right
- Typically 4-8 activities

### Step 2: Add Stories Under Activities
Ask: "What does the user need to do during this activity?"
- Place story cards vertically under each activity
- Most essential at top, nice-to-haves below
- Use color coding for priority

### Step 3: Identify Walking Skeleton
Ask: "What's the minimum viable journey?"
- Look at top row of stories across all activities
- Must Haves = walking skeleton
- Draw line below to separate from enhancements

### Step 4: Review Flow
Ask: "Does this tell the user's story left to right?"
- Read across the top: Does it make sense?
- Read down each column: Right priority order?
- Any gaps in the journey?

---

## Common Patterns

### Authentication Flow
1. **Discover** → 2. **Sign Up** → 3. **Log In** → 4. **Use App** → 5. **Manage Account** → 6. **Recover Access**

### E-commerce Flow
1. **Browse** → 2. **Search** → 3. **Select Product** → 4. **Add to Cart** → 5. **Checkout** → 6. **Track Order**

### SaaS Onboarding Flow
1. **Discover** → 2. **Sign Up** → 3. **Setup** → 4. **First Use** → 5. **Invite Team** → 6. **Upgrade**

---

## Anti-Patterns (Avoid These)

❌ **Organizing by persona instead of journey**
- Wrong: "New User" column, "Returning User" column
- Right: Journey flows left to right for all personas

❌ **Organizing by technical layer**
- Wrong: "Frontend" column, "Backend" column, "Database" column
- Right: User activities, with technical stories underneath

❌ **Too many activities**
- Wrong: 15+ activities (too granular)
- Right: 4-8 major activities (keep it simple)

❌ **No vertical prioritization**
- Wrong: Random order of stories under activities
- Right: Must haves at top, nice-to-haves below

❌ **Cards overlapping**
- Wrong: Insufficient spacing causes overlap
- Right: 400px horizontal, 170px vertical spacing

---

## AI Story Mapping Workflow

When creating a story map from stories:

1. **Analyze stories** - Identify natural user journey flow
2. **Extract activities** - Group stories by user goals/steps
3. **Sequence activities** - Order chronologically left to right
4. **Organize stories** - Place under appropriate activity by priority
5. **Apply spacing** - Use consistent spacing to avoid overlap
6. **Mark walking skeleton** - Identify NOW line if enough stories exist

---

## Example: Iteration-1 Authentication

**Activities** (left to right):
1. Discover App (infrastructure setup)
2. Sign Up (registration flow)
3. Log In (authentication)
4. Use App (landing page)
5. Manage Account (profile management)
6. Recover Access (password reset)

**Walking Skeleton (NOW)**:
- All infrastructure (STORY-001 to 004)
- Registration (STORY-005, 012)
- Login (STORY-006, 011)
- Password Reset (STORY-007)
- Landing Page (STORY-010)

**Later**:
- Email Verification (STORY-013)
- Remember Me (STORY-008)
- Account Management (STORY-009)

---

## Tips for Workshops

**Facilitating with team**:
1. Start with activities - get agreement on journey flow
2. Brainstorm stories - sticky notes for each activity
3. Prioritize vertically - move essential stories up
4. Draw the NOW line - agree on walking skeleton
5. Identify gaps - look for missing steps

**Remote collaboration**:
- Use Miro's voting features for prioritization
- Assign different colors to team members
- Use frames to organize discussion topics
- Take screenshots for documentation

---

## Integration with Product Discovery

**When to create story map**:
- **After synthesis** - Visualize journey before extracting stories
- **After story extraction** - Organize existing stories by journey
- **During workshop** - Collaborate with team to build journey

**Sync with markdown**:
- Story map markdown file documents the journey
- Miro board is the visual collaboration layer
- Both should stay in sync via `/map` command

---

## References

- Jeff Patton's "User Story Mapping" book
- Focus on user's journey (horizontal)
- Focus on priority (vertical)
- Walking skeleton = minimal viable journey
