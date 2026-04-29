# humanizer-pro

Agent skill. 39 constraints for writing text that doesn't read like AI output. Composition-time rules, not post-hoc editing. Works with any agentic framework that supports SKILL.md.

## What it does

Most "humanizer" tools work backward: you write with an LLM, then run the output through a filter that swaps words and restructures sentences. The result still reads like processed AI text, just with different vocabulary.

This skill works forward. It loads 39 constraints before writing starts and applies them per-sentence during composition. The output is written human from the first draft, not cleaned up after the fact.

## How it works

Five phases run in sequence:

1. **Calibration** locks the voice profile (register, perspective, stance, audience) before any writing begins. Optionally calibrates from a writing sample to mirror the user's existing voice.
2. **Composition** applies all 39 constraints as active rules. Each sentence is shaped by them during generation, not checked against them afterward.
3. **Voice injection** adds the things constraint-following alone can't produce: sentence rhythm variation, opinion insertion, concrete specifics, deliberate imperfection.
4. **Verification** runs four passes: a grep-based pattern scan for known AI tells, a structural audit (sentence length variance, paragraph openers, confidence variation, noun-verb ratio), an introspective self-audit ("what makes this still sound AI?"), and a read-aloud test.
5. **Final output** delivers clean text with no meta-commentary about the process.

## The 39 constraints

Seven categories. Priority-tiered so the model knows where to spend attention.

**Content (C1-C8):** No significance inflation, notability puffing, participial filler, promotional tone or persuasive authority tropes, vague attributions, formulaic sections, title-as-proper-noun openings, or hallucinated citations.

**Language (C9-C14):** No AI vocabulary words (33-word kill list drawn from Kobak et al.'s excess frequency analysis, plus "actually"), copula avoidance, negative parallelisms or tailing negations, forced rule-of-three, synonym cycling, or false ranges.

**Style (C15-C20):** Em dash discipline (max 1 per 500 words), boldface restraint, no inline-header lists, sentence case headings, no emojis, no unnecessary tables.

**Communication (C21-C25):** No chatbot artifacts, knowledge-cutoff disclaimers, sycophancy, chatbot tracking artifacts (utm_source, oaicite, citeturn), and straight quotes only.

**Filler/Hedging (C26-C28):** No filler phrases (13-entry kill-and-replace map), no hedging stacks, no generic positive endings.

**Epistemic/Structural (C29-C35):** Vary confidence levels across claims, write from a situated perspective instead of an omniscient one, vary sentence predictability (burstiness), favor verbs over nominalizations, don't replace narrative with bulleted lists, name researchers instead of anthropomorphizing research, and vary style across sections of long pieces.

**Voice/Form (C36-C39):** No passive voice that hides the actor or subjectless ad-copy fragments, no uniform hyphenation across common compound modifiers (third-party, cross-functional, data-driven), no pedagogical signposting ("Let's dive in"), no fragmented headers (header → restating one-liner → real content).

## Installation

### Any SKILL.md-compatible framework

Clone or copy `SKILL.md` into your framework's skill directory. The file is self-contained with standard SKILL.md frontmatter.

```bash
git clone https://github.com/OWNER/humanizer-pro.git /path/to/your/skills/humanizer-pro
```

### Claude Code

```bash
git clone https://github.com/OWNER/humanizer-pro.git ~/.claude/skills/humanizer-pro
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
2. 39 constraints instead of 29. The additional 10 come from peer-reviewed stylometric research published in 2024-2025 (noun-verb ratio distortion, burstiness deficit, cross-segment uniformity, register rigidity), the lmmx AI Tells Rubric (view from nowhere, uniform confidence, anthropomorphized research, colon-list elision), and original constraints (title-as-proper-noun openings, hallucinated citations, unnecessary tables, chatbot tracking artifacts). C36-C39 are ported from upstream blader/humanizer 2.5.1 (passive voice, hyphenated word pair overuse, signposting announcements, fragmented headers).
3. Four-pass verification catches anything that slipped through composition. The grep patterns cover 18+ pattern groups. The structural audit checks 10 properties. The self-audit asks the holistic "what still smells AI?" question. The read-aloud test catches what the others miss.

## Agent configuration

`CLAUDE.md` and `AGENTS.md` in this repo contain recommended operational instructions for proactive skill activation. They do not activate anything automatically. Copy the config block from either file into your agent's own instructions to enable proactive detection of public-facing writing tasks.

## Sources

The constraint set draws from eight primary sources:

- [blader/humanizer](https://github.com/blader/humanizer) v2.5.1 (MIT, Siqi Chen). Upstream 29-pattern catalog. Direct port for C36-C39; supplemental augments for C9 ("actually"), C11 (tailing negations), and C4 (persuasive authority tropes).
- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (April 2026 revision). WikiProject AI Cleanup. Covers 8 major categories. Basis for C1-C8, C10-C13, C15-C21, C23-C26, C28.
- Kobak et al. (2024). Excess word frequency in LLM output vs. human baselines. 329 statistically overused words. Top 10 integrated into C9.
- Reinhart (PNAS 2025). Noun-to-verb ratio distortion in LLM text. Basis for C32.
- Tripto et al. (EMNLP 2025). Cross-segment stylistic uniformity as a detection signal. Basis for C29, C35.
- DivEye (2025). Burstiness deficit (low perplexity variance) in LLM output. Basis for C31.
- Yakura et al. (2024). Cultural feedback loop words amplified by RLHF. Integrated into C9.
- lmmx AI Tells Rubric. Community catalog of 30+ epistemic tells. Basis for C30, C33, C34.
- Dentella & Wang (EMNLP 2025). Register rigidity in LLM output. Supporting evidence for C35.

## License

MIT
