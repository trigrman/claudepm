# Extract User Stories from Discovery Synthesis (with Acceptance Criteria)

Please review the synthesis document(s) and extract well-formed user stories with comprehensive acceptance criteria, ready for development and issue tracker import.

## Required Input
**Iteration**: [Specify the iteration, e.g., `2025-11-mvp`]
**Starting Story ID**: [Next available ID based on scanning all iterations]

## Context Files to Review
- `product/context/product-overview.md` (for product scope and constraints)
- `product/context/target-users.md` (for persona details)
- `product/context/technical-context.md` (for technical constraints affecting AC)
- **`product/iterations/[ITERATION]/discovery/synthesis/synthesis-[MOST-RECENT-DATE].md`** (the MOST RECENT synthesis for this iteration - use only this, older synthesis files are historical record only)
- `product/iterations/[ITERATION]/design/` (for screenshots and design requirements)
- Existing stories in all `product/iterations/*/stories/` (to avoid duplication and understand existing stories)

## Instructions

### Story Creation
1. Review the "Required System Capabilities" section from the iteration's synthesis
2. Review the `product/iterations/[ITERATION]/design/` directory for screenshots and design artifacts
3. **Check for existing stories**: Review stories in all iterations to see if similar stories already exist
4. Create user stories based on:
   - **Synthesis capabilities**: Business requirements and user needs from synthesis
   - **Design screens**: Often each screen or major UI component represents a story
   - **Hybrid approach**: Some stories may be pure functionality, others may be screen-focused
5. Follow the standard user story format: "As a [persona], I want to [action], so that [benefit]"
6. Use **general personas** appropriate to your product (not specific stakeholder names)
7. Add story points or t-shirt sizing if enough context exists
8. Include traceability back to the synthesis (which user needs this addresses)
9. **Include screenshot references** where screens exist
10. **Document the iteration** in each story's Source section
11. Flag any stories that need additional discovery or clarification

### Business vs Technical Requirements
- **Focus on business requirements**: What the system must do from a user perspective
- **Include obvious technical requirements**: When business requirement clearly implies technical need (e.g., "mobile-responsive" from synthesis requirement for mobile use)
- **Avoid prescriptive technical details**: Don't specify tech stack, architecture, or implementation approach unless explicitly required by business constraints

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

## Output Location
Create individual story files in: `product/iterations/[ITERATION]/stories/`

Use naming convention: `story-[number]-[short-description].md`

Example: `product/iterations/2025-11-mvp/stories/story-001-user-login.md`

If the stories directory doesn't exist yet, create it.

## Story Template
Use the appropriate template based on development approach:
- `product/templates/story-template-llm-dev.md` for LLM-centric development
- `product/templates/story-template-human-dev.md` for human-centric development

Key elements to include:

```markdown
# User Story: [Story Title]

**Story ID**: STORY-[Number]
**Priority**: [Must have/Should have/Could have/Won't have]
**Status**: [Draft/Ready/Built]
**Labels**: [iteration-name], [persona-name], [feature-area]

## User Story
As a [general persona],
I want to [action],
So that [benefit/outcome].

## Source
**Iteration**: [e.g., 2025-11-mvp]
**Synthesis Reference**: [Which synthesis document(s)]
**User Need**: [The JTBD this addresses]
**Supporting Evidence**: [Role descriptions from synthesis, not specific names]

## Design Reference
*(Include this section if design artifacts exist)*
**Screenshots**:
- [Path to relevant screenshot]

**Design Notes**: [Any specific design requirements visible in screenshots]

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

### Non-Functional Requirements
- [ ] Performance: [Specific requirement]
- [ ] Security: [Specific requirement]
- [ ] Accessibility: [Specific requirement]
- [ ] Usability: [Specific requirement]

### Quality Checklist
- [ ] Tests written and passing
- [ ] Documentation updated
- [ ] Code reviewed
- [ ] Accessibility tested

## Technical Notes
[Any technical considerations, constraints, or dependencies]

## Estimate
**Size**: [XS/S/M/L/XL or story points]
**Confidence**: [High/Medium/Low]

## Dependencies
- [Other stories or work that must be completed first]
```

## Success Criteria
- [ ] Each story follows standard format (As a... I want... So that...)
- [ ] Persona uses general descriptions appropriate to your product
- [ ] No specific stakeholder names in stories
- [ ] Benefit is clear and measurable
- [ ] **Comprehensive acceptance criteria generated** with Given-When-Then scenarios
- [ ] **All scenarios covered**: happy path, error cases, edge cases
- [ ] **Non-functional requirements specified**: performance, security, accessibility
- [ ] Acceptance criteria are specific, measurable, and testable
- [ ] **Screenshots referenced** where design artifacts exist
- [ ] **Design requirements captured** from prototype/screenshots
- [ ] Traceability to most recent synthesis is maintained
- [ ] Focus on business requirements with obvious technical needs included
- [ ] Stories are small enough to complete in one iteration (if not, note need to split)
- [ ] Technical feasibility is considered (flag blockers)
- [ ] Labels include iteration name for easy filtering
- [ ] Both synthesis capabilities AND design screens reviewed for story creation
- [ ] Story numbering is sequential across ALL iterations (never reset)

## Story Sizing Guidelines
- **XS**: < 1 day, minimal complexity, clear implementation
- **S**: 1-2 days, some complexity, mostly clear
- **M**: 3-5 days, moderate complexity, may need design discussion
- **L**: 1-2 weeks, high complexity, requires architecture decisions
- **XL**: > 2 weeks, very high complexity - should be split into smaller stories

## Output Summary
After creating all story files:

1. **Create stories-index.md** in the iteration's stories directory:
   - List all stories created with their IDs and titles
   - Summary of priorities
   - Total effort estimate

2. **Report to user**:
   - Total stories created
   - Distribution by priority
   - Any stories flagged for additional discovery
