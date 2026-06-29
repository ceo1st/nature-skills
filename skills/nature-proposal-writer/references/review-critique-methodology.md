# Review Critique Methodology

## When to Load

Use this reference when the user asks you to **evaluate** an existing review/survey paper for quality — not to write one, but to assess critical depth, narrative coherence, analytical voice, and research gap insight.

Load alongside the base `researchwrite` SKILL.md. This reference provides the evaluation framework; the base SKILL provides the research context (domain defaults, project structure, etc.).

## 6-Dimension Evaluation Framework

Score each dimension on a 1-10 scale, then report per-dimension scores alongside an overall score. Each dimension has specific signals to look for.

### D1: Synthesis vs Literature Stacking

**What to check**:
- Does the review just list findings ("Person A found X; Person B found Y; Person C found Z") or does it build a conceptual framework?
- Are contradictions between studies identified and discussed? Or papered over?
- Does the author propose their own organization of the field (a taxonomy, a phase model, a paradigm narrative)?
- **Red flag**: Sections that are pure reference-by-reference recitation with zero connective analysis.
- **Positive signal**: An explicit meta-narrative — "School A vs School B", "Phase 1 → Phase 2 paradigm shift" — constructed by the author, not borrowed from a single cited paper.

### D2: Causal Chain Coherence

**What to check**:
- Trace the logical chain from fundamentals to applied outcomes. For corrosion/materials reviews, the canonical chain is: `melt chemistry → oxide film formation → failure mechanisms → control strategies`.
- Are all links present? If "failure" is described only implicitly within "formation", that's a missing link.
- Is the chain qualitative or quantitative? Are critical thresholds, transition criteria, or phase boundaries given?
- **Red flag**: The chain is assumed but never explicitly traced. Reader must infer the connections.
- **Positive signal**: A single explicit equation or block diagram connecting all stages.

### D3: Classification Systems (e.g., Failure Modes)

**What to check**:
- Do the proposed categories emerge naturally from the data/mechanisms? Or are they forced / artificial?
- Within each category: are conditions, thresholds, and sub-mechanisms analyzed? Or just listed?
- Do categories have clear boundaries, or do they overlap?
- Are interactions between categories discussed (e.g., "does mechanism A accelerate mechanism B?")?
- **Red flag**: Categories are enumerated but each gets only a sentence. No individual analysis.
- **Red flag**: "Four failure modes" claimed but the text only discusses one or two in any depth.

### D4: Author's Analytical Voice

**What to check**:
- Can you find sentences where the author makes a **judgment** (not just reports)? ("This evidence is weak because...", "The field overlooks...", "This claim exceeds what the data support.")
- Does the author take positions on contested issues? Or stay safely neutral?
- Are limitations of cited works called out, or just described neutrally?
- **Red flag**: The review reads like an annotated bibliography — paragraph after paragraph of "X reported Y. Z reported W." with zero authorial framing.
- **Positive signal**: The author names what is missing, what is overclaimed, or what the field is getting wrong — then backs it up.

### D5: Research Gaps Discussion

**What to check**:
- Is the gaps section **structured** (organized by dependency, priority, or sub-field)? Or just "more research is needed"?
- Are gaps **derived from the review's own analysis**? Or generic talking points?
- Are gaps **prioritized**? (Which are most urgent? Which are prerequisites for others?)
- Are concrete **research paths or roadmaps** proposed?
- **Positive signal**: Gaps organized by dependency hierarchy (hardware → methodology → application → engineering), with explicit priority assessment.

### D6: Overstatement and Over-Extrapolation

**What to check**:
- Absolute or superlative language: "most", "best", "first", "only", "always", "never", "唯一", "最", "首次"
- Claims that exceed the evidence base cited (e.g., one study positioned as representing the whole field)
- Overly precise quantitative claims without qualifiers: error bars, condition ranges, applicability limits
- **Red flag**: Author's narrative commitment drives stronger claims than the data support.
- **Positive signal**: Author explicitly qualifies claims with conditions, ranges, and confidence levels.

## Scoring Scale

| Score | Meaning |
|:----:|---------|
| 9-10 | Field-defining synthesis. Minor flaws at most. |
| 7-8 | Strong synthesis with clear authorial voice. Some sections weaker. |
| 5-6 | Adequate — reports literature accurately but adds limited analysis. |
| 3-4 | Mostly literature stacking; author absent from the narrative. |
| 1-2 | Annotated bibliography or error-ridden. |

## Paragraph-Level Citation Format

Always cite specific line ranges or section numbers. Use this format:

> **Section X (lines M-N)**: [quote or paraphrase of the problem passage]
> **Problem**: [specific analytical issue]
> **What's missing / what's weak**: [what a critic would demand]

**Bad**: "Section 3 is weak. The discussion is shallow."
**Good**: "Section 3.1.4 (lines 1341-1361): Describes the bilayer oxide structure but presents it as settled fact. Does not address whether higher-resolution characterization (APT, HRTEM) has revealed finer structure, or whether contradictory reports exist. Reads as uncritical recitation of a single established model."

## Output Format

Provide critique as:

1. **Overall Score**: X/10 (note the document title and scope)
2. **Individual Dimension Scores**: Table:

   | Dimension | Score | Key Issue |
   |:----------|:-----:|:----------|
   | D1: Synthesis vs Stacking | 7.5 | ... |
   | D2: Causal Chain | 7.0 | ... |
   | D3: Classifications | 3.5 | ... |
   | D4: Author Voice | 6.0 | ... |
   | D5: Research Gaps | 8.5 | ... |
   | D6: Overstatement | 7.0 | ... |
   | **Overall** | **6.5** | |

3. **Section-by-Section Issues**: Paragraph-level citations with specific line references
4. **Constructive Recommendations**: Actionable fixes for the author

## Chinese-Language Search Strategy

When the review title is in Chinese, finding the document may take several attempts. Follow this order:

1. **GBrain semantic search** — use `mcp_gbrain_query` with Chinese keywords from the title. Add keywords like 综述/review, 硝酸盐/nitrate.
2. **GBrain keyword search** — use `mcp_gbrain_search` with subset keywords if semantic search returns empty.
3. **Filesystem find** — search the vault paths: `/mnt/e/HermesWork/JL_wiki/`, `/mnt/e/HermesWork/JL_codex_work/`, `/mnt/e/HermesWork/outputs/`. Use `grep -rl` with Chinese keywords.
4. **Windows filesystem** — if not in vault, check `/mnt/c/Users/<username>/`.
5. **Format handling** — Chinese review files may be .md, .docx, or .pdf.
   - For .docx: check with `file` command. Warn user before converting with pandoc (some users block large file conversions).
6. **TOC scan** — once found, read the table of contents (section headings) to locate relevant sections. For documents 5000+ lines, target reading to the sections matching the user's questions. Chinese reviews often use `**bold**` for subsection titles (not `###` headings) and explicit numbering like `3.1.4`.

## Pitfalls

- **The title on the file may not match the user's title exactly.** The actual review may have a broader scope than what the user asks about. Focus on the relevant sections.
- **Don't skip the TOC scan on long documents.** 8000-line reviews require targeted reading.
- **Don't confuse "has an opinion" with "has rigorous analysis".** A strong authorial voice is good, but only if backed by evidence cited in the review.
- **Don't give uniformly high scores** — identify specific strengths AND weaknesses. A credible critique shows nuance.
- **Don't stop at one file location.** The user's vault may have copies in raw/, wiki/, and outputs/ — always check the most recent copy.
- **For .docx files, ask before converting** — pandoc conversions can be blocked by the user.
- **Watch for implicit failure mode classification.** A review may discuss multiple failure mechanisms (spallation, dissolution, Cl⁻ breakdown, Cr depletion) without ever enumerating them as "four failure modes." This is itself a criticism worth noting.
