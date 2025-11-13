# Synthesize Discovery Research

Please analyze the interview files for a specific discovery cycle and create a synthesis document following the template structure.

## Required Input
**Discovery Cycle**: [Specify the cycle directory, e.g., `2025-03-mobile-experience`]

## Context Files to Review
- All files in `product/context/` (for product background)
- All files in `product/discovery/[CYCLE-NAME]/interviews/` (except the template file)
- **All files in `product/discovery/[CYCLE-NAME]/observations/`** - Read every file and incorporate into synthesis
- All files in `product/discovery/[CYCLE-NAME]/surveys/`
- `product/requirements/stories-by-cycle.md` (to see what's already been discovered)
- Previous cycle synthesis documents (to understand previous cycles)

### Handling Observations
Observations may include analytics data, screenshots, competitive analysis, support tickets, or other artifacts:
1. **Read every file** in the observations directory
2. **If an observation is unclear**, ask the PM a blocking question immediately to understand it
3. **If the PM defers answering**, document it in the "Open Questions" section
4. **Incorporate observations** into themes, pain points, and features alongside interview evidence

## Instructions
1. Read all research files in the specified cycle directory
2. Identify recurring themes across interviews (mentioned in 3+ interviews = significant theme)
3. Extract user needs in "Jobs to Be Done" format (When I... I want to... So I can...)
4. Rank pain points by:
   - Frequency (how many participants mentioned it)
   - Impact (High/Medium/Low based on participant descriptions)
5. Propose potential features/user stories based on evidence
6. Note any conflicting feedback or open questions
7. Provide specific interview references for every claim
8. **Cross-reference with previous cycles**: Note if findings confirm, contradict, or expand on previous research

## Output Location
Save the synthesis to: `product/discovery/[CYCLE-NAME]/synthesis-[YYYY-MM-DD].md`

Use today's date in the filename and the cycle directory name provided.

## Output Format
Use the synthesis template structure found at: `product/discovery/synthesis/synthesis-template.md`

## Success Criteria
- Every theme is supported by specific interview references (file names and participant IDs)
- User stories trace back to user needs with evidence
- Priority recommendations are evidence-based (cite frequency and impact)
- Open questions are clearly identified for future research
- No assumptions or inferences without clear supporting evidence from interviews
- Conflicting or minority opinions are noted, not dismissed
- **Cross-cycle insights**: Connections to previous research are noted
- **New vs. confirming**: Clear distinction between new findings and validation of previous cycles

## Quality Checks
- [ ] Each theme references at least 3 interviews
- [ ] Pain points are ranked with quantitative support (X of Y participants)
- [ ] Each proposed feature includes validation evidence
- [ ] **All observation files have been read and incorporated**
- [ ] **Blocking questions were asked for unclear observations**
- [ ] Open questions are listed for any ambiguous findings (including deferred observation questions)
- [ ] Executive summary accurately reflects detailed findings
- [ ] Cross-references to previous cycles are included where relevant
- [ ] Synthesis notes which findings are new vs. confirming previous research

## Post-Synthesis Actions
After creating the synthesis:
1. Review if any existing stories in `stories-by-cycle.md` should be updated
2. Document any contradictions with previous research in the synthesis
