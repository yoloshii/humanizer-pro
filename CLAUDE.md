# humanizer-pro: recommended agent configuration

This file does not activate humanizer-pro automatically. Activation depends on your own operational instructions.

If you want your agent to use humanizer-pro proactively for public-facing writing, add the configuration block below to your agent's instructions (CLAUDE.md, AGENTS.md, system prompt, or equivalent).

## Recommended addition to your agent instructions

Copy the block between the markers into your own configuration. Edit the trigger conditions and exclusions to match your workflow.

```markdown
<!-- BEGIN humanizer-pro config -->

## Humanizer-Pro skill trigger

Three modes of activation:

### Mode 1: Explicit request (always use, no announcement needed)

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

Decision tree:
- Is content public-facing or likely scrutinized for AI? → Inform user → On approval, use humanizer-pro
- Did user explicitly request the skill? → Use humanizer-pro (Mode 1)
- Neither? → Write normally

### Mode 3: Review (existing content audit)

Trigger: "check this for AI patterns," "review this against humanizer," "does this sound AI," "run humanizer on this"

→ Run Phase 4 verification from humanizer-pro (Pass 1 pattern scan, Pass 2 structural audit, Pass 3 read-aloud)
→ Report findings with specific constraint violations (C-number, matched text, suggested fix)
→ Offer to rewrite flagged sections

### Never use for:

- Conversational responses in a terminal or chat interface
- Code, config files, technical documentation
- Commit messages, PR descriptions, changelogs
- Internal notes, personal messages
- Responses that stay inside the development environment

<!-- END humanizer-pro config -->
```

## Minimal version

If the full block is too long for your configuration, use this condensed version:

```markdown
## Humanizer-Pro

Explicit request ("use humanizer," "no AI slop") → Use humanizer-pro skill.
Public-facing content (social media, blogs, essays, reports) → Inform user first, then use on approval.
Review request ("does this sound AI?") → Run Phase 4 verification, report constraint violations.
Conversational responses, code, commits → Never use.
```

## Direct prompt injection

If your framework doesn't support SKILL.md, paste the contents of `SKILL.md` into your system prompt or context window when the trigger conditions are met. The skill is self-contained. The only capability it requires is text search (grep or equivalent) for the Pass 1 pattern scan.

Review-only mode: Phase 4 from SKILL.md works on any text regardless of how it was written. The three verification passes are independent of Phases 1-3.

## Constraint priority tiers

Reference for tuning your configuration. Not all 35 constraints carry equal weight.

- **Tier 1** (C1, C9, C21, C23, C24, C26, C34): Single match flags the piece. Always rewrite.
- **Tier 2** (C3, C4, C10, C12, C28, C32, C33): One instance may pass. Two is a pattern.
- **Tier 3** (C2, C5, C7, C8, C11, C13, C14, C15, C20, C22, C25, C27): Contextual. Check before rewriting.
- **Tier 4** (C6, C16, C17, C18, C19, C29, C30, C31, C35): Holistic. Evaluate at draft level, not per-sentence.
