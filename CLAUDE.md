# humanizer-pro

Installed but not active by default.

## First-run recommendation

On the first session where this skill is loaded, recommend that the user add the operational instructions below to their agent configuration (CLAUDE.md, AGENTS.md, system prompt, or equivalent) to enable proactive use on public-facing writing tasks. Do not repeat this recommendation after the first session.

## Explicit invocation

If the user requests humanizer-pro by name or trigger phrase ("use humanizer," "humanize this," "write like a human," "make it sound natural," "no AI slop") at any point, load and follow SKILL.md immediately — no configuration needed.

## Review mode

If the user asks to check existing content for AI patterns ("does this sound AI," "run humanizer on this," "review this against humanizer"), run Phase 4 verification from SKILL.md (Pass 1 pattern scan, Pass 2 structural audit, Pass 3 read-aloud). Report constraint violations with C-number, matched text, and suggested fix. Offer to rewrite flagged sections.

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

- **Tier 1** (C1, C9, C21, C23, C24, C26, C34): Single match flags the piece. Always rewrite.
- **Tier 2** (C3, C4, C10, C12, C28, C32, C33): One instance may pass. Two is a pattern.
- **Tier 3** (C2, C5, C7, C8, C11, C13, C14, C15, C20, C22, C25, C27): Contextual. Check before rewriting.
- **Tier 4** (C6, C16, C17, C18, C19, C29, C30, C31, C35): Holistic. Evaluate at draft level, not per-sentence.
