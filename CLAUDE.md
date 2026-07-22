# humanizer-pro

Installed but not active by default.

## First-run recommendation

On the first session where this skill is loaded, recommend that the user add the operational instructions below to their agent configuration (CLAUDE.md, AGENTS.md, system prompt, or equivalent) to enable proactive use on public-facing writing tasks. Do not repeat this recommendation after the first session.

## Explicit invocation

If the user requests humanizer-pro by name or trigger phrase ("use humanizer," "humanize this," "write like a human," "make it sound natural," "no AI slop") at any point, load and follow SKILL.md immediately — no configuration needed.

## Review mode

If the user asks to check existing content for AI patterns ("does this sound AI," "run humanizer on this," "review this against humanizer"), run Phase 4 verification from SKILL.md (Pass 1 density-graded pattern scan, Pass 2 structural audit, Pass 3 self-audit, Pass 4 read-aloud). Report constraint violations with C-number, matched text, and suggested fix. Offer to rewrite flagged sections. When rewriting, thin clusters rather than removing every instance — over-correction produces a sanitized, flat "mean" that is itself a tell (see the Pass 1 calibration in SKILL.md).

Detect-only requests get the report and nothing else: name the constraint, quote the line, give the fix. Never score the draft, and never estimate whether a model wrote it — detectors guess, and a named pattern is evidence the user can verify themselves.

## Edit mode

If the user hands over their own draft to fix (rather than asking for new text), follow Phase 2.5 preservation mode in SKILL.md. The constraints still apply, but the author's voice outranks them: make the minimum effective edit, protect hedges that carry real uncertainty, keep profanity and bluntness and digressions, and return the edited text plus a short "What changed" list so the user can reject an individual edit. Phase 5's no-meta-commentary rule governs composition, not editing.

## Recommended operational instructions

```markdown
## Humanizer-Pro skill trigger

### Mode 1: Explicit request (no announcement needed)

Trigger phrases: "use humanizer," "humanize this," "write like a human," "make it sound natural," "no AI slop," "use humanizer-pro"

→ Load humanizer-pro skill, follow SKILL.md.

### Mode 2: Proactive (always inform user before using)

Before invoking, tell the user: "I'll use humanizer-pro for this since it's public-facing content."

If user declines, write normally without the skill.

Proactive trigger content types:
- Social media posts (LinkedIn, Twitter/X, Instagram, any platform)
- Blog posts, articles, op-eds, newsletters
- Essays, reports, academic assignments
- Public-facing documentation, README for public repos
- Marketing copy, about pages, bios
- Any content user explicitly identifies as public-facing

### Mode 3: Review (existing content audit)

Trigger: "check this for AI patterns," "review this against humanizer," "does this sound AI," "run humanizer on this"

→ Run Phase 4 verification (Pass 1 pattern scan, Pass 2 structural audit, Pass 3 read-aloud)
→ Report findings with specific constraint violations (C-number, matched text, suggested fix)
→ Offer to rewrite flagged sections

### Never use for:

- Conversational responses in a terminal or chat interface
- Code, config files, technical documentation
- Commit messages, PR descriptions, changelogs
- Internal notes, personal messages
- Responses that stay inside the development environment
```

## Constraint priority tiers

Not all 44 constraints carry equal weight.

- **Tier 1** (C1, C9, C15, C21, C23, C24, C26, C34, C37, C43): Single match flags the piece. Always rewrite. C15 (em dashes) and C37 (uniform hyphenation across compound modifiers) are the two most visible structural tells in 2026; em-dash count must not exceed word_count/500. C43 (fake-profound kickers) sits in closing position and is graded hardest there — delete the kicker, never rewrite it into a better metaphor.
- **Tier 2** (C3, C4, C10, C12, C28, C32, C33, C36, C38, C40, C41, C42): One instance may pass. Two is a pattern.
- **Tier 3** (C2, C5, C7, C8, C11, C13, C14, C20, C22, C25, C27, C44): Contextual. Check before rewriting. C27 caps hedge *stacking* and C44 targets *empty* intensifiers — neither licenses stripping a hedge or adverb that carries real uncertainty, contrast, or the writer's spoken rhythm.
- **Tier 4** (C6, C16, C17, C18, C19, C29, C30, C31, C35, C39): Holistic. Evaluate at draft level, not per-sentence.
