# humanizer-pro

Agent skill. 44 constraints for writing text that doesn't read like AI output. Composition-time rules first, with a preservation mode for editing drafts you didn't write. Works with any agentic framework that supports SKILL.md.

## What it does

Most "humanizer" tools work backward: you write with an LLM, then run the output through a filter that swaps words and restructures sentences. The result still reads like processed AI text, just with different vocabulary.

This skill works forward. It loads 44 constraints before writing starts and applies them per-sentence during composition. The output is written human from the first draft, not cleaned up after the fact.

When the input is an existing draft rather than a writing task, preservation mode inverts the priority: the constraints still apply, but the author's voice outranks them.

## How it works

Five phases run in sequence:

1. **Calibration** locks the voice profile (register, perspective, stance, audience) before any writing begins. Optionally calibrates from a writing sample to mirror the user's existing voice.
2. **Composition** applies all 44 constraints as active rules. Each sentence is shaped by them during generation, not checked against them afterward.
3. **Voice injection** adds the things constraint-following alone can't produce: sentence rhythm variation, opinion insertion, concrete specifics, deliberate imperfection.
4. **Verification** runs four passes: a grep-based pattern scan for known AI tells (graded HIGH/MED/LOW by density and position, not mere presence, with hits inside quotes and code discarded first), a structural audit (sentence length variance, paragraph openers, confidence variation, noun-verb ratio, plus a substance spot-check that runs deletion and inversion micro-tests on the weakest paragraphs), an introspective self-audit ("what makes this still sound AI?"), and a read-aloud test. A calibration rule keeps editing proportional: thin clusters rather than scrubbing every instance, because over-correction collapses prose into a flat, equally-detectable "mean."
5. **Final output** delivers clean text with no meta-commentary about the process.

**Phase 2.5 (preservation mode)** replaces phases 1-3 when you hand the skill a draft to fix instead of a piece to write. It makes the minimum effective edit, protects hedges and profanity and digressions that carry the author's voice, leaves quoted material verbatim, restores laundered specifics before sanding surface patterns, and returns the edited text plus a short "What changed" list ending in a claims audit ("Claims added: 0", so an edit pass can never quietly invent a fact). Detect-only requests get a report and no rewrite: each constraint that fired, the line it fired on, the fix, and a "Not flagged" list showing what was deliberately left alone and why. Never a score, and never a guess about whether a model wrote it. Style-evidenced flags on non-native English writing get a stricter bar, because detectors measurably over-flag ELL writers.

## The 44 constraints

Eight categories. Priority-tiered so the model knows where to spend attention.

**Content (C1-C8):** No significance inflation, notability puffing, participial filler, promotional tone or persuasive authority tropes, vague attributions, formulaic sections, title-as-proper-noun openings, or hallucinated citations.

**Language (C9-C14):** No AI vocabulary words (33-word kill list drawn from Kobak et al.'s excess frequency analysis, plus "actually", plus a hype/marketing register list for promotional copy), copula avoidance, negative parallelisms or tailing negations, forced rule-of-three, synonym cycling, or false ranges.

**Style (C15-C20):** Em dash discipline (max 1 per 500 words), boldface restraint, no inline-header lists, sentence case headings, no emojis, no unnecessary tables.

**Communication (C21-C25):** No chatbot artifacts, knowledge-cutoff disclaimers, sycophancy, chatbot tracking artifacts (utm_source, oaicite, citeturn), and straight quotes only.

**Filler/Hedging (C26-C28):** No filler phrases (22-entry kill-and-replace map), no hedging stacks, no generic positive endings. C27 caps stacking rather than banning hedges, so a single hedge carrying real doubt survives.

**Epistemic/Structural (C29-C35):** Vary confidence levels across claims, write from a situated perspective instead of an omniscient one, vary sentence predictability (burstiness), favor verbs over nominalizations, don't replace narrative with bulleted lists, name researchers instead of anthropomorphizing research, and vary style across sections of long pieces.

**Voice/Form (C36-C39):** No passive voice that hides the actor or subjectless ad-copy fragments, no uniform hyphenation across common compound modifiers (third-party, cross-functional, data-driven), no pedagogical signposting ("Let's dive in"), no fragmented headers (header → restating one-liner → real content).

**Rhetorical staging and register (C40-C44):** No faux-insight setups ("what nobody tells you"), no colon reveals ("The best part: it learns"), no rhetorical setups or self-answered questions ("So why did it fail? Pricing."), no fake-profound kickers (the closing aphorism, which gets deleted rather than rewritten into a better metaphor), no empty intensifiers (just, simply, literally, obviously, kept when they carry emphasis, contrast, or spoken rhythm).

## Installation

### Any SKILL.md-compatible framework

Clone or copy `SKILL.md` into your framework's skill directory. The file is self-contained with standard SKILL.md frontmatter.

```bash
git clone https://github.com/yoloshii/humanizer-pro.git /path/to/your/skills/humanizer-pro
```

### Claude Code

```bash
git clone https://github.com/yoloshii/humanizer-pro.git ~/.claude/skills/humanizer-pro
```

Or upload `SKILL.md` via the Claude web UI at Settings > Capabilities > Skills > Add. The frontmatter uses the compatible format (space-delimited `allowed-tools` string, `version` under `metadata:`).

### Direct prompt injection

If your framework doesn't support SKILL.md, paste the file contents into your system prompt or context window. The skill is self-contained and only requires text search (grep or equivalent) for the Pass 1 pattern scan. File read/write is optional.

## Usage

The skill activates when the agent is asked to write something. Three ways to trigger it:

**Explicit:** Say "use humanizer" or "write this like a human" or "no AI slop" in your prompt.

**Proactive:** If the agent's operational instructions include the recommended config from `CLAUDE.md`/`AGENTS.md`, it will suggest using the skill when content is public-facing (blog posts, social media, essays, reports). It asks before activating. See `CLAUDE.md` for the recommended configuration block.

**Review:** Say "check this for AI patterns" or "does this sound AI-generated" and it runs the verification phase against existing text, reporting specific constraint violations.

### What it's for

Reports, articles, blog posts, essays, feedback documents, academic assignments, marketing copy, public-facing documentation. Anything where a reader might suspect AI wrote it.

### What it's not for

Terminal responses, code, config files, commit messages, internal notes.

## How it differs from blader/humanizer

The popular [humanizer](https://github.com/blader/humanizer) skill (MIT, Siqi Chen) is a post-hoc editing checklist. You write text, then review it against the checklist and fix violations. As of v2.5.1 (April 2026) it has 29 patterns drawn primarily from the Wikipedia source, plus a voice-calibration option.

This skill has three differences:

1. Constraints are applied during composition, not after. The model doesn't write freely and then self-edit. It writes with the constraints loaded as active rules from the first word.
2. 44 constraints instead of 29. Ten come from peer-reviewed stylometric research published in 2024-2025 (noun-verb ratio distortion, burstiness deficit, cross-segment uniformity, register rigidity), the lmmx AI Tells Rubric (view from nowhere, uniform confidence, anthropomorphized research, colon-list elision), and original constraints (title-as-proper-noun openings, hallucinated citations, unnecessary tables, chatbot tracking artifacts). C36-C39 are ported from upstream blader/humanizer 2.5.1 (passive voice, hyphenated word pair overuse, signposting announcements, fragmented headers). C40-C44 are derived from petergyang/no-ai-slop (faux-insight setups, colon reveals, rhetorical setups, fake-profound kickers, empty intensifiers), whose catalog covers rhetorical staging patterns the encyclopedic sources miss.
3. Four-pass verification catches anything that slipped through composition. The grep patterns cover 23+ pattern groups. The structural audit checks 10 properties. The self-audit asks the holistic "what still smells AI?" question. The read-aloud test catches what the others miss.
4. A preservation mode for editing text you didn't write. The composition constraints assume you control every sentence. When the input is someone else's draft, that assumption inverts. The author's voice outranks the constraint set, and a technically clean rewrite that no longer sounds like them is a failure.

## Agent configuration

`CLAUDE.md` and `AGENTS.md` in this repo contain recommended operational instructions for proactive skill activation. They do not activate anything automatically. Copy the config block from either file into your agent's own instructions to enable proactive detection of public-facing writing tasks.

## Sources

The constraint set draws from thirteen primary sources:

- [blader/humanizer](https://github.com/blader/humanizer) v2.5.1 (MIT, Siqi Chen). Upstream 29-pattern catalog. Direct port for C36-C39; supplemental augments for C9 ("actually"), C11 (tailing negations), and C4 (persuasive authority tropes).
- [petergyang/no-ai-slop](https://github.com/petergyang/no-ai-slop) (MIT, Peter Yang), July 2026. Editing-mode skill organized around voice preservation. Basis for C40-C44, the C9 hype-register list, the C26 filler-opener additions, Phase 2.5 preservation mode, and the detect-only doctrine.
- [AgriciDaniel/anti-slop](https://github.com/AgriciDaniel/anti-slop) (Apache-2.0 code, CC BY-SA 4.0 marker references), July 2026. A defect-verification toolkit, deliberately not a humanizer; studied as adversarial prior art. Basis for the quoted-text standing rule, the substance spot-check, the claims audit, the "Not flagged" list, the ELL bar, and the corrected C15 rationale.
- Czuma (2026). Pre-registered corpus study of em-dash prevalence in 69,632 medRxiv preprints; population-level indicator, not a per-document detector. Basis for the corrected C15 rationale.
- Stowe et al. (ACL 2026). Detector demographic bias: 16 models over-flag English-language-learner essays while human annotators on the same essays showed no significant demographic bias. Basis for the ELL bar in detect-only mode.
- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (April 2026 revision). WikiProject AI Cleanup. Covers 8 major categories. Basis for C1-C8, C10-C13, C15-C21, C23-C26, C28.
- Kobak et al. (2024). Excess word frequency in LLM output vs. human baselines. 329 statistically overused words. Top 10 integrated into C9.
- Reinhart (PNAS 2025). Noun-to-verb ratio distortion in LLM text. Basis for C32.
- Tripto et al. (EMNLP 2025). Cross-segment stylistic uniformity as a detection signal. Basis for C29, C35.
- DivEye (2025). Burstiness deficit (low perplexity variance) in LLM output. Basis for C31.
- Yakura et al. (2024). Cultural feedback loop words amplified by RLHF. Integrated into C9.
- lmmx AI Tells Rubric. Community catalog of 30+ epistemic tells. Basis for C30, C33, C34.
- Dentella & Wang (EMNLP 2025). Register rigidity in LLM output. Supporting evidence for C35.

## Changelog

### v2.4.0

Hardened against the failure modes a defect-verification toolkit (AgriciDaniel/anti-slop) documents in humanizer-class tools. No new constraints; the count stays at 44.

- **Quoted text is off-limits.** A new standing rule binding every phase: a watched phrase that is quoted, mentioned, or discussed is not a hit. Pass 1 discards matches inside quotes, blockquotes, and code before grading density. Closes a real bug class where a draft quoting someone's words, or discussing AI patterns, would get its quotes restyled.
- **Substance spot-check in Pass 2.** Deletion and inversion micro-tests on the weakest paragraphs: cut the most abstract sentence and name what was lost; negate each significance claim and ask if anyone would assert the negation. A draft can pass all 44 constraints and still say nothing; this is the guard against fluent emptiness.
- **Claims audit in preservation mode.** The "What changed" list now ends with "Claims added: 0". Any fact, name, number, or date not in the source and not from the user is an invention to remove. An edit pass changes how things are said, never what is claimed.
- **"Not flagged" list in detect-only mode**, naming the patterns deliberately not reported and why. Restraint becomes visible instead of indistinguishable from a miss.
- **ELL bar.** Style-evidenced flags on non-native English writing need a higher bar, not a lower one (Stowe et al., ACL 2026: detectors over-flag ELL essays, while human annotators in the same study showed no significant bias). Isolated style flags are suppressed; only clusters of three or more independent signals get reported.
- **C15 rationale corrected.** The unsourced "3-10x the rate of human writers" multiplier is gone; the constraint now cites the one pre-registered measurement (Czuma 2026) together with its own caveat that em-dash rate is a population-level indicator, not a per-document detector. The cap survives as reader-perception discipline.
- **C26 human-signals gate.** "In order to" and its neighbors sit on Wikipedia's observed list of *human*-writing signals; stripping every instance moves text toward the generated register. The kill-and-replace map is now a default for stacks, not an absolute.
- **C11 gains the reversed straw-alternative form** ("X rather than Y" where nobody proposed Y), and **C27 the sharper repair rule**: when the hedged claim is vacuous, cut the claim, not the hedge.

### v2.3.0

- **Five new constraints (C40-C44), a new category: rhetorical staging and register.** C40 faux-insight setups ("what nobody tells you"), which flatter the writer rather than the reader. C41 colon reveals ("The best part: it learns"), manufactured suspense in running prose, distinct from C33's colon-list elision and C17's bullet headers. C42 rhetorical setups and self-answered questions ("So why did it fail? Pricing."). C43 fake-profound kickers, promoted straight to Tier 1, because the closing aphorism is the most reliably AI-shaped sentence in a piece; the handling rule is *delete, do not improve*. C44 empty intensifiers, conditional by design: kept when they carry emphasis, contrast, or spoken rhythm.
- **Phase 2.5 preservation mode.** The composition constraints assume you control every sentence; editing someone else's draft inverts that. Minimum effective edit, an explicit protect-list (hedges carrying real doubt, profanity, digressions, uneven polish, the author's own repeated vocabulary), specificity restored before surface sanded, and an output contract that suspends Phase 5: edited text plus a short "What changed" list, so the user can reject an individual edit.
- **Detect-only doctrine.** A request to check a draft without rewriting it returns named constraints, quoted lines, and fixes. No score, no percentage, no guess about whether a model wrote it. Detectors guess; a named pattern is evidence the user can verify.
- **C27 carve-out.** The hedging constraint caps *stacking*, it does not ban hedges. Reduce a stack to one; never take the last one. Resolves a real conflict with C29 (vary your confidence) that previously let a technically-passing edit strip an author's honest uncertainty.
- **Hype/marketing register added to C9.** The existing list skews encyclopedic-academic because its sources are Wikipedia and Kobak et al. Promotional copy fails in a different register with almost no overlap: empower, supercharge, elevate, transformative, game-changing, unleash, seamless, effortless, plus stock reactions ("this is huge", "this changes everything").
- **Nine filler openers added to C26**, including the near-pure-filler "when it comes to" and "in terms of", and the undated "in today's world" family.
- Sources list corrected from "eight" to the actual count.

### v2.2.0

- **Density-graded Pass 1.** Pattern-scan hits are scored HIGH/MED/LOW by frequency-per-1000-words and position (openings weighted hardest) and rewritten worst-first — operationalizing the co-occurrence principle the skill already states.
- **"Thin, don't shave" calibration.** An explicit guard against over-correction: stripping every tell collapses prose into a sanitized regression-to-the-mean voice that is itself a tell. Bites hardest in review/rewrite mode. Converging evidence from community (kambleakash0/english-humanizer) and academic (pedrohcgs detect-only `/humanize`) skills.
- **Era-versioned C9 vocabulary.** The AI-vocabulary note is annotated by model era (GPT-4 / GPT-4o / GPT-5), with the principle that structural constraints (C3, C11, C12, C36) outlast lexical ones and the word list needs periodic re-baselining; adds context-dependent watch-words (streamline, utilize, harness, paradigm, synergy, bolstered).

## License

MIT
