# Extract User Stories from Discovery Synthesis (with Acceptance Criteria)

Please review the synthesis document(s) and extract well-formed user stories with comprehensive acceptance criteria, ready for development and issue tracker import.

## Required Input
**Discovery Cycle**: [Specify the cycle, e.g., `2025-03-mobile-experience`]
**Starting Story ID**: [Next available ID based on stories-by-cycle.md]

## Context Files to Review
- `product/context/product-overview.md` (for product scope and constraints)
- `product/context/target-users.md` (for persona details)
- `product/context/technical-context.md` (for technical constraints affecting AC)
- `product/discovery/[CYCLE-NAME]/synthesis-[DATE].md` (the synthesis for this cycle)
- `product/requirements/stories-by-cycle.md` (to avoid duplication and understand existing stories)
- Previous cycle synthesis documents (to understand the broader context)

## Instructions

### Story Creation
1. Review the "Potential Features/Stories" section from the cycle's synthesis
2. **Check for existing stories**: Review stories-by-cycle.md to see if similar stories already exist
3. For each feature, create one or more detailed user stories OR update existing stories
4. Follow the standard user story format: "As a [persona], I want to [action], so that [benefit]"
5. Add story points or t-shirt sizing if enough context exists
6. Include traceability back to the synthesis (which user needs this addresses)
7. **Document the discovery cycle** in each story's Source section
8. Flag any stories that need additional discovery or clarification

### Acceptance Criteria Generation
For EACH story, generate comprehensive acceptance criteria:

**Functional Scenarios** (Given-When-Then format):
- Happy path scenarios
- Error/failure scenarios
- Edge cases
- Validation requirements

**Non-Functional Requirements**:
- Performance (response time, load handling)
- Security (authentication, authorization, data protection)
- Accessibility (WCAG compliance, keyboard navigation, screen readers)
- Usability (error messages, user feedback)

**Quality Criteria**:
- What constitutes "done" for this story
- Testing requirements
- Documentation needs

## Handling Existing Stories
If a finding relates to an existing story:
- Create an entry in `product/requirements/changes/YYYY-MM-[cycle-name]-changes.md`
- Document what changed and why
- Update the existing story file with new information
- Add a note in the story about which cycle updated it

## Output Location
Create individual story files in: `product/requirements/[CYCLE-NAME]/`

Use naming convention: `story-[number]-[short-description].md`

Example: `product/requirements/2025-10-onboarding-flow/story-001-user-login.md`

If the cycle directory doesn't exist yet, create it.

## Story Template
Use this format for each story file (compatible with common issue trackers):

```markdown
# User Story: [Story Title]

**Story ID**: [Number]
**Epic**: [Epic name if known]
**Priority**: [Must have/Should have/Could have/Won't have]
**Status**: [Draft/Ready/In Progress/Done]
**Labels**: [discovery-cycle-name], [persona-name], [feature-area]

## User Story
As a [persona],
I want to [action],
So that [benefit/outcome].

## Source
**Discovery Cycle**: [e.g., 2025-03-mobile-experience]
**Synthesis Reference**: [Which synthesis document(s)]
**User Need**: [The JTBD this addresses]
**Supporting Evidence**: [Interview references from synthesis]

## Change History
*(Add entries when story is updated from later cycles)*
- **[YYYY-MM-DD]**: Updated from cycle [cycle-name] - [Brief description of change]

## Acceptance Criteria

### Functional Scenarios

**Scenario 1: [Scenario Name - Happy Path]**
- **Given** [initial context/precondition]
- **When** [action occurs]
- **Then** [expected outcome]
- **And** [additional outcome if needed]

**Scenario 2: [Scenario Name - Error Case]**
- **Given** [initial context]
- **When** [error condition occurs]
- **Then** [expected error handling]
- **And** [user feedback provided]

**Scenario 3: [Scenario Name - Edge Case]**
- **Given** [edge condition]
- **When** [action occurs]
- **Then** [expected behavior]

### Non-Functional Requirements
- [ ] Performance: [Specific requirement, e.g., "Response time < 2s"]
- [ ] Security: [Specific requirement, e.g., "User authentication required"]
- [ ] Accessibility: [Specific requirement, e.g., "WCAG 2.1 AA compliant"]
- [ ] Usability: [Specific requirement, e.g., "Clear error messages displayed"]

### Quality Checklist
- [ ] Unit tests written and passing
- [ ] Integration tests cover main scenarios
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] Accessibility tested
- [ ] Performance validated
- [ ] [Criterion 3]

## Technical Notes
[Any technical considerations, constraints, or dependencies]

## Open Questions
- [Any uncertainties that need resolution]

## Estimate
**Size**: [XS/S/M/L/XL or story points]  
**Confidence**: [High/Medium/Low]

## Dependencies
- [Other stories or work that must be completed first]
```

## Success Criteria
- [ ] Each story follows standard format (As a... I want... So that...)
- [ ] Persona is specific (from target-users.md)
- [ ] Benefit is clear and measurable
- [ ] **Comprehensive acceptance criteria generated** with Given-When-Then scenarios
- [ ] **All scenarios covered**: happy path, error cases, edge cases
- [ ] **Non-functional requirements specified**: performance, security, accessibility
- [ ] Acceptance criteria are specific, measurable, and testable
- [ ] Traceability to synthesis is maintained
- [ ] Stories are small enough to complete in one iteration (if not, note need to split)
- [ ] Technical feasibility is considered (flag blockers)
- [ ] Labels include cycle name for easy filtering

## Story Sizing Guidelines
- **XS**: < 1 day, minimal complexity, clear implementation
- **S**: 1-2 days, some complexity, mostly clear
- **M**: 3-5 days, moderate complexity, may need design discussion
- **L**: 1-2 weeks, high complexity, requires architecture decisions
- **XL**: > 2 weeks, very high complexity - should be split into smaller stories

## Output Summary
After creating all story files:

1. **Update `product/requirements/stories-by-cycle.md`**:
   - Add a new section for this cycle
   - List all stories created with their file paths
   - Document key insights from the cycle
   - Update the overview counts

2. **If any existing stories were updated**:
   - Document changes in the story's "Change History" section
   - Note which cycle prompted the update
