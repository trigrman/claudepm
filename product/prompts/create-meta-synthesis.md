# Create Meta-Synthesis Across Iterations

Please analyze multiple iterations to identify patterns, contradictions, and strategic insights.

## Purpose

A meta-synthesis connects insights across iterations to:
- Identify persistent themes and patterns
- Track how understanding has evolved
- Spot contradictions that need resolution
- Uncover strategic opportunities
- Guide product direction and prioritization

## When to Create a Meta-Synthesis

- **Quarterly**: Every 3 months to review all iterations
- **Thematic**: When multiple iterations explored related topics
- **Pre-planning**: Before roadmap planning sessions
- **Validation**: When a pattern appears across iterations

## Context Files to Review

Required:
- All synthesis documents from the iterations being analyzed (in `product/iterations/*/discovery/synthesis/synthesis-*.md`)
- Stories from all iterations (to see how insights translated to requirements)

For context:
- `product/context/product-overview.md`
- `product/context/target-users.md`

## Instructions

1. **Identify iterations to analyze**
   - List all iterations in scope (date range, thematic group, or all iterations)
   - Note the focus of each iteration

2. **Extract themes from each synthesis**
   - Read the "Key Themes" section from each synthesis
   - Create a master list of all themes

3. **Identify cross-iteration patterns**
   - Which themes appear in multiple iterations?
   - How has understanding of each theme evolved?
   - What new insights emerged from later iterations?

4. **Find contradictions**
   - Where do iterations disagree?
   - Can contradictions be explained by context, segment, or timing?
   - What needs further validation?

5. **Track assumption validation**
   - Which assumptions were confirmed?
   - Which were invalidated?
   - How did this change product direction?

6. **Identify emerging opportunities**
   - What strategic insights emerge from connecting iterations?
   - What opportunities weren't visible in single iterations?

7. **Make recommendations**
   - Product direction guidance
   - Feature prioritization insights
   - Future research needs

## Output Location

Save to: `product/discovery/meta-synthesis/meta-[TIMEPERIOD-OR-THEME].md`

Examples:
- `meta-2025-q1.md` (quarterly review)
- `meta-mobile-experience.md` (thematic across mobile-focused iterations)
- `meta-onboarding-evolution.md` (tracking one area over time)

## Output Format

Use the template at: `product/discovery/meta-synthesis/meta-synthesis-template.md`

## Analysis Checklist

- [ ] All relevant iterations are included
- [ ] Cross-iteration themes are identified with references to specific iterations
- [ ] Theme evolution is tracked chronologically
- [ ] Contradictions are noted and analyzed
- [ ] Assumptions are categorized as validated/invalidated/unknown
- [ ] Strategic opportunities are identified
- [ ] Recommendations are evidence-based
- [ ] Research gaps are clearly articulated
- [ ] Feature priority guidance includes rationale

## Success Criteria

A good meta-synthesis:
- Reveals patterns not visible in individual iterations
- Provides strategic product direction guidance
- Identifies what's been validated vs. what needs more research
- Connects dots between seemingly separate findings
- Guides future discovery priorities
- Helps with roadmap planning and prioritization

## Example Usage

**Quarterly review:**
```bash
claude-code --context product/iterations/2025-01-*/discovery/synthesis/synthesis-*.md \
  --context product/iterations/2025-02-*/discovery/synthesis/synthesis-*.md \
  --context product/iterations/2025-03-*/discovery/synthesis/synthesis-*.md \
  product/prompts/create-meta-synthesis.md
```

**Thematic analysis:**
```bash
claude-code --context product/iterations/*-mobile-*/discovery/synthesis/synthesis-*.md \
  --context product/iterations/*-tablet-*/discovery/synthesis/synthesis-*.md \
  product/prompts/create-meta-synthesis.md
```

## Post-Meta-Synthesis Actions

1. Share with product/leadership team
2. Use insights for roadmap planning
3. Identify priority gaps for next iterations
4. Update product strategy documentation if major insights emerged
5. Consider whether any existing stories need re-prioritization
