# Review Paper Framework Design — Gap-Driven Approach

## When to Use

When JL asks to design a review/survey paper framework from a research topic, especially for:
- Domain literature reviews (e.g., "综述硝酸盐腐蚀")
- Sub-topic focused reviews with a specific lens (e.g., "聚焦氧化膜形成与失效")
- Papers destined for Corrosion Science, SolMat, or equivalent journals

Distinct from `compose-mode.md` which covers proposals/original research plans. This reference covers the **pre-writing framework design** phase for review papers.

## Workflow: Gap-Driven Design

### Phase 1: Literature Landscape Assessment

**Tool routing for maximum coverage:**

| Source | Tool | Purpose |
|--------|------|---------|
| GBrain vault | `gbrain_query` + `gbrain_search` + `gbrain_get_page` | Existing curated notes, chapter drafts, reference lists |
| Zotero | `zotero_search_items` (everything mode) | Stored papers with metadata |
| Web | `web_search` (multiple query variants) | Papers not in local DB |
| Full-text | `web_extract` on PDF URLs | Key paper details |

**Search strategy:** Run GBrain + Zotero + web in **parallel** on the first pass — each has independent latency. Then cascade: expand terms, target specific gaps.

### Phase 2: Gap Identification

After Phase 1, enumerate explicit gaps. Each gap must be:
1. A specific question that the review can address
2. Mapped to existing vs. missing literature
3. Scored by importance to the review's narrative

Example from this session:
```
Gap 1: 氧化膜失效定量判据 (spallation critical stress, thickness vs failure probability)
Gap 2: NaNO₂对氧化膜组成的影响
Gap 3: 氧化膜剥落-再生循环演化
Gap 4: >10000h长时间尺度数据
Gap 5: 熔盐化学指标(pO²⁻) → 氧化膜寿命定量模型
```

### Phase 3: Targeted Gap Filling

For each gap, design specific search queries. Use web_search with exact phrases and author names, not just generic keywords. Extract promising PDFs with web_extract.

**Honest gap labeling:** If a gap cannot be filled after thorough searching, label it as a **field-level gap** — not a search failure. This becomes a legitimate contribution of the review (identifying research frontiers).

### Phase 4: Literature Count Assessment

Before designing the framework, do an honest count. Rule of thumb:
- **Corrosion Science / SolMat review**: 80-150 references expected
- **~50 or fewer**: review is thin, need more targeted searching
- **~75-85**: solid for a 30,000-word focused review

Present the count by category so JL can judge coverage.

### Phase 5: Causal-Chain Narrative Design

Core principle: **don't organize by material or research group. Organize by mechanism level.**

Design a causal chain that runs through the entire paper:
```
Root cause → Intermediate process → Observable consequence → Engineering impact
```

Example for oxide layer review:
```
熔盐化学状态(pO²⁻, NaNO₂) → 氧化膜生长热力学/动力学 → 氧化膜结构/组成 → 失效模式触发 → 工程后果
```

Each section in the framework maps to one link in the chain.

### Phase 6: Section Contracting

For each section, define:
- **Purpose**: what question does this section answer?
- **Inputs**: which literature feeds this section?
- **Allowed claims**: what can be asserted here?
- **Forbidden claims**: what belongs in another section?
- **Key references**: the 3-5 most critical citations

### Phase 7: Default Review Structure

A proven 7-section template for materials/corrosion reviews:

| Section | Role | ~Words |
|---------|------|--------|
| 1. Introduction | Problem framing + scope boundary | 2,500 |
| 2. Environmental context | The "weather" that drives the phenomenon | 4,000 |
| 3. Formation mechanism | How the thing forms (structure, kinetics) | 5,000 |
| 4. Failure modes ★ | Academic增量所在 — systematic classification + quantitative criteria | 8,000 |
| 5. Controlling factors | What determines the fate (links §2 ↔ §4) | 4,000 |
| 6. Methodology | How we "see" the phenomenon (toolbox chapter) | 3,000 |
| 7. Engineering implications + outlook | Translation to practice + research gaps | 3,000 |

§6 (methodology) should be retained as a standalone section — it serves readers who need to evaluate literature evidence quality. Do not dissolve into other sections.

### Phase 10: Table-as-Figure Substitution

When a conceptual diagram resists clean rendering — too much "AI味", infographic style mismatched with academic journal conventions, or information density too high for a figure — **replace it with a table**. Tables have zero style conflict, are directly citable by reviewers, and can carry equal or greater information density.

Decision rule:
- Structural diagrams (oxide bilayer, failure mode grid) → GPT image generation
- Causal chains, theory comparisons, data-rich process flows → **table**
- If GPT generates 3 versions and all feel "off" → **table**

Example from this session: Fig 2 (causal chain from salt chemistry to oxide failure) went through 3 GPT generations, all with infographic artifacts. Replaced by Table 1 (5 rows × 5 columns: Stage, Chemical Process, Key Reaction/Criterion, Effect on Oxide Scale, Reference). Cleaner and more citable.

### Pitfalls

1. **Organizing by research group** ("Lab X did A, Lab Y did B") — reads like a book report, not a synthesis
2. **Organizing by material** ("304 corrodes like X, 316 like Y") — misses cross-cutting mechanisms
3. **Treating gaps as search failures** — some absences are genuine field-level gaps; labeling them is a contribution
4. **Skipping the count assessment** — JL needs to know if the literature base is sufficient before committing to writing
5. **Over-designing before Phase 1** — let the literature landscape shape the framework, not vice versa
6. **Metaphors in section titles** — Chinese academic reviews must use scientific titles only. No "命运", "总开关", "大气", "看见" in any heading. Titles are structural signposts, not narrative rhetoric. See `references/chinese-review-writing-style.md` for the full naming convention.
7. **Missing first-line indent** — when generating .docx for Chinese academic papers, body paragraphs MUST have `first_line_indent = Cm(0.74)`. Headings, figure captions, and references are exempt. This is a formatting requirement, not optional.

### Phase 8: Figure Strategy for Review Papers

**Three-source rule:** No single method covers all figure types for a materials/corrosion review.

| Figure type | Method | Example |
|------------|--------|---------|
| Conceptual diagrams (structures, failure modes, causal chains) | GPT image generation via `image_generate` | Oxide bilayer, 2×2 failure grid |
| Data curves, bar charts, tables, theory comparisons | SVG via `concept-diagrams` skill | Wagner theory, methodology matrix |
| Empirical evidence (SEM, XRD, mass loss curves) | Direct capture from published papers | Goods 2004 mass loss vs time |

**GPT image generation for academic figures — critical constraints:**
- Prompt must specify "academic journal figure style, no decorative elements, no icons, no gradients, no shadows, plain white background"
- Do NOT use words like "infographic" or "illustration" — produces non-academic visual style
- GPT works for: structural diagrams, comparison grids, process flows
- GPT fails for: data charts (hallucinates numbers), tables (misaligns), mathematical notation
- Always verify with `vision_analyze` before accepting
- Figure captions and citations should NOT be in the generated image — add separately

**Honesty rule:** Do not create "conceptual" figures that look like data. If a figure is synthesized from multiple sources without a single empirical source, label it clearly as "概念综合图" with supporting references.

**Tightened boundaries from iteration (2026-06-23 session):**

| Figure type | Use GPT? | Why |
|------------|:---:|------|
| Structural/cross-section diagrams | ✅ | Fig 1 (oxide bilayer) worked well |
| 2×2 comparison grids | ✅ | Fig 3 (failure modes) worked well |
| Data bar/column charts | ❌ | GPT bar charts look AI-ish, prefer literature capture or clean SVG |
| Conceptual phase diagrams (T-pO²⁻, etc.) | ❌ | If no published paper has drawn it, the review shouldn't either. JL cut Fig 8 for this reason. Either find a published source or do not include |
| Theory comparison tables | ❌ | SVG via concept-diagrams skill; GPT misaligns tables |
| Causal chain flowcharts | ⚠️ mixed | Fig 2 took 3 versions before acceptable. If SVG is clean enough, prefer SVG |

**Figure iteration expectation:** Figure strategy typically takes 2-3 rounds — SVG draft → GPT attempt → user feedback → final mix. Don't expect first attempt to land. JL will reject AI-infographic-looking figures and figures without literature precedent. Present each round as options: "SVG version, GPT version, or capture from published paper?"

**New pitfall (Phase 8):**
6. **Creating figures that imply empirical support where none exists** — if a phase diagram, relationship curve, or quantitative map has no published source, either find one or remove the figure entirely. A review paper's figures must be traceable to published data or labeled as conceptual synthesis.
7. **Causal chains that span 5+ stages → prefer tables** — if a GPT-generated flowchart looks "AI-ish" or infographic-like after 2+ iterations, switch to a table. Tables avoid visual style mismatches and are directly citable by reviewers. Each row can carry a literature reference in the last column. See session example: Fig 2 was replaced by Table 1.
8. **Figure placement must mirror citation location** — do not batch all figures at the end of a section. Each figure belongs at the exact paragraph where it is first discussed. If a figure is cited in §3.2 but was placed in §4.5, move it.

### Phase 9: Chinese Review Paper Writing Style

Chinese academic reviews differ from proposals. Key rules beyond `research-anti-slop.md`:

**Structural rules:**
- Each paragraph carries exactly ONE point. Short paragraphs (3-5 sentences) are preferred
- No "随着...的发展" openings — start with substance
- No filler transitions: 值得注意的是, 毫无疑问, 众所周知, 具有重要意义
- No formulaic scaffolding: 首先/其次/再次/最后 chains

**Scientific register:**
- Use precise technical terms, not approximate descriptions
- When citing data, give numbers: not "显著增加" but "+285.7%"
- When citing thresholds, give values: not "较高浓度" but "≥0.135 wt%"
- Distinguish fact levels explicitly: 实验显示/数据表明 vs 可能/推测/有待验证

**"AI味" (AI writing smell) — specific patterns to avoid:**
- Overly smooth paragraph transitions that no human academic writes
- Sentences that start with a summary of the previous sentence
- Adjectives used as padding rather than precision
- "不仅...而且..." structures used without logical necessity
- Ending paragraphs with a platitude instead of a specific claim

## Cross-Reference

- After framework is approved, hand off to `compose-mode.md` for actual writing
- Use `professor` skill for domain-expert review of gap analysis
- Use `gbrain-research-lookup` for fact-checking during literature assessment
- Full Chinese review writing style guide: `references/chinese-review-writing-style.md`
