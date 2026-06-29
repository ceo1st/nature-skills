# Worked example: Quaternary chloride proposal revise-mode evaluation

**Date**: 2026-05-11
**Target file**: `/vault/raw/氯盐储能/四元氯盐腐蚀机理研究_修订版.docx`
**Mode**: revise
**Text type**: doctoral proposal, Part 1 (first stage)

## What worked

### Pipeline flow applied
1. Classify text → §1 background+lit review, §2 objectives, §3 methodology (8 subsections), §4 expected outcomes, references
2. Extract claims → each paragraph scanned for key claims, traced to literature or model source
3. Compare with canon → cross-checked against Gong Qing's first-stage constraints (from chloride-salt-first-stage.md)
4. Diagnose structure → found: Mg→Zn purification dilemma is tightest argument chain; §4 is bloated with redundant conditionals
5. Anti-slop scan → checked all 4 structural anti-patterns + 3 language anti-patterns; none triggered seriously
6. Score → 6.9 overall (supervisor-facing threshold met)
7. Revision brief → 2 P0, 3 P1, 4 P2 items

### Scoring applied
Each dimension scored independently with evidence from the text:
- 研究问题清晰度 7: question stated but buried in §1, not standalone
- 科学张力 8: Mg+ZnCl2 displacement reaction creates genuine tension
- 证据匹配 6: simulation liquidus temps reported to 3 sig figs, overstated precision
- 逻辑链 8: Mg→Zn purification chain is tight; minor gap in Q1/Q2/Q3 selection rationale
- 方法可行性 6: purification→sampling→coupon insertion atmosphere control not described; temperature programs not given
- 创新性 6: contribution implicit, no explicit innovation section
- 风险边界 7: conditional outcome logic present but no "all candidates fail" fallback
- 语言质量 7: no serious anti-slop; §4 too long

### Gong Qing constraint checklist
Every constraint from chloride-salt-first-stage.md was checked explicitly:
- Composition selection via simulation figures ✓
- No air exposure experiment ✓
- Material classes not specific grades ✓
- Four offline experiment flows ✓
- Later platform work deferred ✓
- Simulation boundary sentences ✓

## What to watch for

### Pitfall: vision API unavailable
When the vision API is quota-exhausted (common with free-tier Gemini), embedded figures in docx cannot be verified. Workarounds:
- Extract images from docx zip and save to disk for later review
- Use figure captions and surrounding text as proxies for figure content
- Flag "unable to verify figure content" in the evaluation
- Ask JL to confirm figure accuracy separately

### Pitfall: precision inflation
Simulation/model results reported to 3+ significant figures always flag. Check whether the figure axes support that precision — usually they don't. Recommended fix: use "~" notation and +/- ranges.

### Pitfall: purification + coupon insertion gap
Any flow that says "cool → sample → add coupon → re-heat" must describe atmosphere control during intermediate steps. This is the single most common experimental design flaw in offline chloride salt proposals.

## Revision brief format

The template used:

```
## Revision Brief

### P0 (must fix)
1. [Item] — [Why] — [How]

### P1 (strongly recommended)
...

### P2 (suggested optimization)
...
```

Each item includes: specific location in text, the problem, the concrete fix.
