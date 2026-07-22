---
name: humanizer-pro
version: 2.3.0
license: MIT
compatibility: claude-code opencode
description: |
  Generates human-sounding text from scratch using 44 anti-AI-pattern constraints applied during composition, and edits existing drafts without flattening the author's voice. Use when writing reports, analyses, articles, feedback documents, essays, documentation, blog posts, or any substantial text where AI detection is a concern. Also use when user says "write this like a human," "make it sound natural," "no AI slop," or "use humanizer." Handles voice calibration (including writing-sample matching), constraint-driven composition, rhythm variation, opinion injection, specificity passes, a preservation mode for editing someone else's draft, and four-pass automated verification (pattern scan, structural audit, self-audit, read-aloud). Aligned with Wikipedia:Signs of AI writing (April 2026 revision), upstream blader/humanizer 2.5.1, petergyang/no-ai-slop, and peer-reviewed stylometric research (2024-2026).
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Humanizer Pro: Write like a human from the start

## Quick start

1. Determine voice profile (register, perspective, stance, audience). Optionally calibrate from a writing sample (Phase 1A.5).
2. Load 44 anti-pattern constraints as active composition rules
3. Write the piece with constraints applied per-sentence
4. Inject voice: vary rhythm, insert opinions, add specifics, allow imperfection
5. Run four-pass verification: pattern scan (Grep), structural audit, self-audit, read-aloud test
6. Output clean text with no meta-commentary

**Editing someone else's draft instead of composing?** Go to Phase 2.5. The constraints still apply, but the author's voice outranks them, and the output contract changes.

## When to use

- Writing reports, analyses, feedback documents, articles
- Creating content that will be read by humans who might suspect AI
- Any output longer than a paragraph where voice and credibility matter
- Proactively, before you start writing, not after

## Phase 1: Calibration (before writing)

Before drafting a single sentence, establish these parameters.

### 1A. Determine voice profile

Ask yourself four questions about the piece:

| Question | Options |
|----------|---------|
| **Register** | Formal / Technical / Conversational / Mixed |
| **Perspective** | First person singular / First person plural / Third person / Shifting |
| **Stance** | Opinionated / Balanced-with-opinions / Neutral-reportorial |
| **Audience** | Peers / Decision-makers / General public / Mixed |

Lock these before writing. If the user hasn't specified, infer from context. A feedback report to Chrome developers is Technical + First-plural + Opinionated + Peers. A blog post is Conversational + First-singular + Opinionated + General.

### 1B. Load anti-pattern constraints

These 44 constraints are active during composition. They are not a checklist to run afterward. They shape every sentence as you write it.

Memorize the constraint categories:
- **Content (1-8)**: What you say and how you source it
- **Language (9-14)**: How you construct sentences
- **Style (15-20)**: How it looks on the page
- **Communication (21-25)**: Chatbot artifacts and paste residue
- **Filler/Hedging (26-28)**: Verbal padding
- **Epistemic/Structural (29-35)**: How you think and organize on the page
- **Voice/Form (36-39)**: Specific surface tells from upstream consensus (passive voice, hyphenated pairs, signposting, fragmented headers)
- **Rhetorical staging and register (40-44)**: Manufactured drama and hype vocabulary (faux-insight setups, colon reveals, staged questions, kickers, empty intensifiers)

Not all constraints carry equal weight. During composition, allocate attention by priority:

- **Tier 1 (instant tells, always rewrite)**: C1, C9, C15, C21, C23, C24, C26, C34, C37, C43. A single hit from any of these is enough to flag a piece. These are the patterns detectors and human reviewers catch first.
- **Tier 2 (strong signals, rewrite on sight)**: C3, C4, C10, C12, C28, C32, C33, C36, C38, C40, C41, C42. One instance may pass; two in the same piece is a pattern.
- **Tier 3 (contextual, check before rewriting)**: C2, C5, C7, C8, C11, C13, C14, C20, C22, C25, C27, C44. These are legitimate in some contexts. Flag them, but don't blindly rewrite.
- **Tier 4 (holistic, assess in structural audit)**: C6, C16, C17, C18, C19, C29, C30, C31, C35, C39. These can't be caught per-sentence. Evaluate at the draft level in Pass 2.

**Instruction-layer note:** These instructions use structured lists, bold labels, tables, colon-prefixed items, and uniformly authoritative tone. This formatting is optimized for LLM instruction parsing. Do not replicate it in output. The constraints below govern what you write for the user, not how these instructions are formatted.

### 1A.5. Voice calibration from a writing sample (optional)

If the user provided a writing sample (their own previous writing, or a target voice), read it before drafting. Match the sample's surface features rather than imposing a generic "natural" voice.

When you read the sample, note:

- **Sentence length patterns** — short and punchy? Long and flowing? Mixed cadence? What is the typical range?
- **Word choice level** — casual ("stuff", "thing"), academic ("artifact", "construct"), or somewhere between? Don't upgrade their casual words to formal ones in the rewrite.
- **Paragraph openings** — do they jump straight in, or set context first? Mirror that pattern.
- **Punctuation habits** — lots of dashes, parenthetical asides, semicolons? Match their punctuation rhythm (subject to the C15 em dash cap).
- **Recurring phrases or verbal tics** — preserve them. If they always write "I keep thinking about", let it appear in the rewrite.
- **Transitions** — do they use explicit connectors ("So,", "Anyway,") or just start the next point? Don't add transitions they wouldn't.

When matching their voice, do not just remove AI patterns — replace them with patterns from the sample. If they write short sentences, do not produce long ones. If they use "stuff" and "things", don't promote those to "elements" and "components".

When no sample is provided, fall back to the default voice profile from 1A and the personality guidance in Phase 3.

**How users supply samples:**

- Inline: "Humanize this. Here's a sample of my writing for voice matching: [text]"
- File: "Humanize this. Use my writing style from [path] as a reference."

### 1C. Prime the rhythm

Write a throwaway opening sentence that is deliberately short. Under 8 words. This anchors your rhythm. If your first sentence is 30 words long, the whole piece drifts toward uniform long sentences.

---

## Phase 2: Composition (active constraints)

Write the piece with all 44 constraints loaded. Each constraint below includes its trigger patterns and what to do instead.

### Content constraints

#### C1. No Significance Inflation

**Kill on sight:** stands/serves as, is a testament/reminder, vital/significant/crucial/pivotal/key role/moment, underscores/highlights importance, reflects broader, symbolizing ongoing/enduring/lasting, setting the stage, indelible mark, deeply rooted

**Instead:** State what happened and what it does. If something is important, the facts will show it. Don't announce importance; demonstrate it.

#### C2. No Notability Puffing

**Kill on sight:** independent coverage, local/regional/national media outlets, music/business/tech outlets, profiled in, active social media presence, maintains an active social media presence, written by a leading expert

**Instead:** Cite one specific source with a specific claim. "A 2024 NYT investigation found X" beats "covered by major media outlets." Don't list sources that covered a topic; summarize what they actually said.

#### C3. No Participial Filler (-ing Phrases)

**Kill on sight:** highlighting/underscoring/emphasizing..., ensuring..., reflecting/symbolizing..., contributing to..., cultivating/fostering..., encompassing..., showcasing..., aligning/resonating with...

**Instead:** End the sentence. Start a new one. The -ing phrase is almost always a second idea crammed onto the first.

#### C4. No Promotional Tone or Persuasive Authority Tropes

**Kill on sight (promotional):** boasts a, vibrant, rich (figurative), profound, enhancing its, exemplifies, commitment to, natural beauty, nestled, in the heart of, groundbreaking (figurative), renowned, breathtaking, must-visit, stunning, a myriad of, shed light on

**Kill on sight (persuasive authority tropes):** the real question is, at its core, in reality, what really matters, fundamentally, the deeper issue, the heart of the matter, in the realm of

**Problem:** LLMs use persuasive authority tropes to pretend they are cutting through noise to some deeper truth. The sentence that follows usually just restates an ordinary point with extra ceremony.

**Before:**
> The real question is whether teams can adapt. At its core, what really matters is organizational readiness.

**After:**
> The question is whether teams can adapt. That mostly depends on whether the organization is ready to change its habits.

**Instead:** Describe concretely. Dimensions, dates, names, numbers. "A 200-seat restaurant that opened in 2019" not "a vibrant dining destination." When tempted to write "the real question is", just write the question. When tempted to write "fundamentally", just state the point.

#### C5. No Vague Attributions or Source Inflation

**Kill on sight:** Industry reports, Observers have cited, Experts argue, Some critics argue, several sources/publications, such as (before exhaustive word lists presented as non-exhaustive)

**Instead:** Name the source. If you can't name it, you don't have it. Drop the claim or find a real citation. Don't present 1-2 sources as "several publications." Don't use "such as" to imply a larger set than actually exists.

#### C6. No Formulaic Structure Sections

**Kill on sight:** Despite its... faces several challenges..., Despite these challenges, Challenges and Legacy, Future Outlook, In conclusion, In summary, Overall

**Instead:** Weave problems and prospects into the narrative where they naturally arise. Don't segregate them into labeled bins. Don't add a summary section that restates what was just said.

#### C7. No Title-as-Proper-Noun Openings

**Kill on sight:** Opening sentences that introduce a topic title as if it were a standalone real-world entity needing formal definition. "X is a [category] that [definition]" when X is not a proper noun.

**Instead:** Start with what matters about the topic. "The 2019 flooding displaced 4,000 residents" not "The 2019 Midwest flooding event is a significant natural disaster that occurred in the central United States."

#### C8. No Hallucinated Citations

**Rule:** Never invent a source, DOI, ISBN, page number, or URL. If you cite a study, name the actual authors and year. If you cite a statistic, know where it came from. If you can't verify it, don't cite it.

**Kill on sight:** Books cited without page numbers, DOIs that look plausible but are fabricated, access-dates that predate the writing context, URLs with `utm_source=openai` or `utm_source=chatgpt.com` or `referrer=grok.com` tracking params

**Instead:** Cite fewer sources with higher confidence. One real source beats three invented ones. If you don't have a source, state the claim without attribution or flag the gap honestly.

### Language constraints

#### C9. No AI Vocabulary Words

**Kill on sight:** Actually, Additionally, align with, comprehensive, crucial, delve, emphasizing, enduring, enhance, exhibited, fostering, garner, highlight (verb), insights, interplay, intricate/intricacies, key (adjective), landscape (abstract), meticulous, multifaceted, notably, particularly, pivotal, realm, showcase, swift, tapestry (abstract), testament, underscore (verb), valuable, vibrant, within (when "in" works)

**Instead:** Use the plainest word that works. "Important" not "crucial." "Show" not "showcase." "Also" not "Additionally." "Thorough" not "comprehensive." "Showed" not "exhibited." Most of these words have simple equivalents. "Actually" almost always means nothing — delete it.

**Note:** "delve" dropped off sharply in 2025 LLM output but remains a strong historical tell. Words like "comprehensive," "notably," "particularly," "within," and "multifaceted" were identified by Kobak et al. (2024) as having the highest excess frequency in LLM output vs. human baselines. Co-occurrence is the real signal: one or two of these words may be coincidence; five in the same piece is not.

**The watch-list ages — track model eras (v2.2.0).** This lexical list drifts by model generation; the *structural* constraints (C3, C11, C12, C36) are far more stable than any word list, so weight them higher and re-baseline this list periodically rather than trusting it forever. Approximate drift:
- **GPT-4 era (2023–2024):** delve, tapestry, testament, intricate, meticulous, beacon, realm.
- **GPT-4o era (2024–2025):** align with, fostering, bolstered, robust, dynamic, multifaceted, leverage, harness, paradigm, synergy.
- **GPT-5 era (2025+):** emphasizing, enhance, highlighting, showcasing, streamline, utilize, interplay, ecosystem, framework, vibrant.

Most are already killed above or by C1/C3/C32. Net additions to watch — **context-dependent**, kill in figurative/gravitas use but allow in genuine technical use (e.g. "software framework", "dynamic programming", "Spark ecosystem"): streamline, utilize, harness, paradigm, synergy, bolstered, ecosystem, framework, dynamic.

**Hype/marketing register (v2.3.0).** The list above skews encyclopedic-academic, because its sources are Wikipedia and Kobak et al. Marketing copy, landing pages, and launch posts fail in a different register, and the words that give them away barely overlap. Kill in promotional use:

empower, supercharge, elevate, embark, transformative, paramount, ever-evolving, facilitate, game changer, game-changing, unlock (figurative), unleash, revolutionize, seamless, effortless, next-level

Also kill the stock reaction phrases that pad launch copy: "this is huge", "this changes everything", "let that sink in".

Same context rule as the era list: these are dead in figurative or gravitas use, fine in literal use. "Unlock the door" is a door. "Facilitate the workshop" is a real job description. "Unlock unprecedented growth" is slop. When you reach for one of these words, name the actual effect instead — what specifically got faster, cheaper, or possible that wasn't before.

#### C10. No Copula Avoidance

**Kill on sight:** serves as, stands as, marks, represents [a], boasts, features, offers [a]

**Instead:** Write "is" or "has." Gallery 825 is the exhibition space. The building has four rooms. Stop flinching from simple verbs.

#### C11. No Negative Parallelisms or Tailing Negations

**Kill on sight (parallelism):** Not only...but..., It's not just about..., it's..., It's not merely...it's..., no..., no..., just...

**Kill on sight (tailing negation):** Clipped fragments tacked onto sentence ends to mimic punchy ad copy. "no guessing", "no wasted motion", "no friction", "no surprises", "no nonsense" appearing as standalone clauses after a comma.

**Before (tailing negation):**
> The options come from the selected item, no guessing.

**After:**
> The options come from the selected item without forcing the user to guess.

**Instead:** State the positive claim directly. "The beat adds aggression" not "It's not just about the beat, it's about the aggression." For tailing negations, expand the fragment into a real clause or rewrite as a positive statement.

#### C12. No Rule-of-Three Forcing

**Kill on sight:** Any list of exactly three items where the third feels forced. "Innovation, inspiration, and industry insights." "Streamlining, enhancing, and fostering."

**Instead:** Use as many items as are real. Two is fine. Four is fine. Three is suspicious when all three are abstract nouns.

#### C13. No Synonym Cycling

**Kill on sight:** The protagonist / the main character / the central figure / the hero (cycling through synonyms for the same referent to avoid repetition)

**Instead:** Repeat the noun. English handles repetition fine. Forced synonym variation reads as algorithm output.

#### C14. No False Ranges

**Kill on sight:** from X to Y constructions where X and Y aren't on a meaningful continuum. "From the Big Bang to the cosmic web, from star birth to dark matter."

**Instead:** List the topics directly. "The book covers the Big Bang, star formation, and dark matter theories."

### Style constraints

#### C15. Em Dash Discipline

**Kill on sight:** Em dashes (—), double-hyphen substitutes ( -- ), and any parenthetical dash separator. LLMs use em dashes at 3-10x the rate of human writers. This is the single most visible structural tell in 2026 output. Readers and detectors flag it before vocabulary or tone.

**Rule:** Maximum one em dash (or double-hyphen substitute) per 500 words. Zero is better. Every time you reach for an em dash, stop and use a period, a comma, or parentheses instead. Rewrite the sentence if needed. Double hyphens in CLI flags (--enable-features) and code are exempt.

**Self-check:** After drafting, count em dashes and double-hyphen separators across the entire piece. If count exceeds (word_count / 500), rewrite until it doesn't. A 1500-word piece gets a maximum of 3. A 500-word piece gets 1. A 200-word Discord post gets 0.

#### C16. Boldface Restraint

**Rule:** Bold only structural headers. Never bold inline phrases for emphasis. If something needs emphasis, rewrite the sentence so the important word lands at the end, where English naturally stresses it.

#### C17. No Inline-Header Lists

**Kill on sight:** Bullet lists where each item starts with a bolded noun followed by a colon. `- **Speed:** faster than...`

**Instead:** Write prose. If a list is genuinely needed, use plain bullets without headers. Or use a table.

#### C18. Sentence Case Headings

**Rule:** Headings use sentence case. "What we found" not "What We Found." Title case is a ChatGPT tell.

#### C19. No Emojis

**Rule:** Never use emojis unless the user explicitly requests them.

#### C20. No Unnecessary Tables

**Rule:** Don't create small tables that would be better as prose. A table needs at least 3 rows and 2 columns to justify its existence. If the data is simple enough to say in a sentence, say it in a sentence.

### Communication constraints

#### C21. No Chatbot Artifacts

**Kill on sight:** I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., is there anything else, let me know, more detailed breakdown, here is a...

**Instead:** Start with the content. No preamble, no sign-off, no offers to expand.

#### C22. No Knowledge-Cutoff or RAG Disclaimers

**Kill on sight:** as of [date], Up to my last training update, While specific details are limited/scarce, based on available information, in the provided/available sources/search results, not widely available/documented/disclosed, maintains a low profile, keeps personal details private

**Instead:** State what you know. If you don't know something, say so plainly: "I couldn't find data on this" or just omit it. Don't speculate about what "likely" exists when you lack sources.

#### C23. No Sycophancy

**Kill on sight:** Great question!, You're absolutely right, That's an excellent point, What a fascinating topic

**Instead:** Respond to the substance. If someone's point is relevant, engage with it. Don't praise it.

#### C24. No Chatbot Tracking Artifacts

**Kill on sight:** `utm_source=openai`, `utm_source=chatgpt.com`, `utm_source=copilot.com`, `referrer=grok.com`, `citeturn0search0`, `contentReference[oaicite:0]`, `oai_citation`, `<grok_card>`, `[attached_file:1]`, `[web:1]`, `({"attribution":{"attributableIndex"`, placeholder URLs like `INSERT_SOURCE_URL`, placeholder dates like `2025-xx-xx`

**Instead:** Strip all tracking parameters from URLs. Never include citation markup artifacts from any chatbot. If you find yourself writing a placeholder, stop and either fill it with real data or remove the reference.

#### C25. Straight Quotes Only

**Rule:** Use straight quotes (`"..."`) not curly quotes. Check before finalizing. Note: ChatGPT and DeepSeek use curly quotes; Claude and Gemini typically do not, but verify anyway.

### Filler/hedging constraints

#### C26. No Filler Phrases

**Kill-and-replace map:**

| Kill | Replace with |
|------|-------------|
| In order to | To |
| Due to the fact that | Because |
| At this point in time | Now |
| In the event that | If |
| Has the ability to | Can |
| It is important to note that | (delete; start with the content) |
| It's important/critical/crucial to note/remember/consider | (delete; start with the content) |
| Worth noting | (delete) |
| At the end of the day | (delete) |
| It goes without saying | (delete; if it goes without saying, don't say it) |
| It bears mentioning | (delete; start with the content) |
| Navigating the complexities of | (delete; say what the complexities are) |
| It is fascinating to note | (delete) |
| When it comes to | (delete; start with the subject) |
| In terms of | (delete, or name the actual dimension) |
| With regard to / With respect to | About, or (delete) |
| In today's world / In the age of / In the world of | (delete; date the claim if it needs dating) |
| The reality is / The truth is | (delete; state the claim) |
| Going forward | (delete, or give the actual date/trigger) |
| In this article / In this post | (delete; C38 territory) |

**Note:** "It's important to note" and "worth noting" were among the strongest AI tells in 2022-2024. They appear less often in 2025+ model output but remain worth catching.

**Note on the openers:** "When it comes to X" and "In terms of X" are near-pure filler — the sentence almost always works with the phrase deleted and X promoted to subject. "When it comes to pricing, we're competitive" becomes "Our pricing is competitive." The "In today's world" family additionally dates a claim without committing to a date; if the timeframe matters, name it.

#### C27. No Excessive Hedging

**Rule:** One hedge per claim maximum. "This may affect outcomes" is fine. "This could potentially possibly be argued to have some effect" is four hedges on one verb.

**Carve-out — this constraint caps stacking, it does not ban hedges.** A single hedge that carries real doubt, softens a request, or reproduces how the writer speaks is doing work, and C29 (vary your confidence) actively wants it there. Reduce a stack to one hedge. Never take the last one.

- ✅ "I think the second approach is better, but I haven't tested it." (one hedge, real uncertainty)
- ✅ "Maybe worth checking before we ship." (softening, spoken register)
- ❌ "It could potentially possibly be argued that this might have some effect." (five hedges, zero content)

This carve-out is load-bearing in preservation mode (Phase 2.5), where stripping an author's honest "I'm not sure" is the most common way an edit destroys their voice while passing every other check.

#### C28. No Generic Positive Endings

**Kill on sight:** The future looks bright, Exciting times lie ahead, continues their journey toward excellence, a major step in the right direction

**Instead:** End with a specific fact, a concrete next step, or an honest uncertainty. "They plan to open two more locations next year" or "Whether this scales remains an open question."

### Epistemic/structural constraints

#### C29. No Uniform Confidence

**Rule:** Vary your certainty level across claims. AI writes everything with the same assertive tone, whether stating a well-documented fact or a speculative interpretation. Humans express doubt on shaky claims and confidence on solid ones.

**Kill on sight:** Every paragraph making claims with equal certainty. No hedges anywhere, or hedges distributed uniformly rather than concentrated where uncertainty is real.

**Instead:** Match confidence to evidence. Strong assertion for solid facts. "Probably" or "it seems like" for weak evidence. "I'm not sure about this, but" for speculation. The mismatch between certainty and evidence quality is the tell. Calibrate it.

#### C30. No View from Nowhere

**Rule:** Write from a situated perspective. AI defaults to an omniscient, disembodied narrator who surveys everything from above. Humans write from a specific vantage point with limited visibility.

**Kill on sight:** Text that describes a situation as if the writer has equal access to all perspectives, all data, and all timeframes simultaneously. Balanced "on one hand / on the other hand" structures that treat every viewpoint as equally weighted.

**Instead:** Acknowledge your vantage point. "From what I've seen," "In our experience," "The data I've looked at suggests." Be positioned. Not biased, but grounded in a specific place with specific access to information.

#### C31. Sentence Burstiness

**Rule:** Vary the predictability of your sentences. AI output has low perplexity variance; every sentence is approximately equally surprising. Human writing oscillates between predictable (simple, setup) and surprising (novel, punchline) sentences.

**Instead:** Mix dead-simple sentences ("It broke.") with dense ones that pack multiple ideas. Let some sentences coast while others do heavy lifting. Uneven when measured, natural when read.

#### C32. Noun-Verb Ratio

**Rule:** Use more verbs and fewer nominalizations. AI output has a measurably higher noun-to-verb ratio than human writing (Reinhart, PNAS 2025). AI prefers "the implementation of" over "we implemented," "the utilization of resources" over "we used resources."

**Kill on sight:** Chains of abstract nouns connected by prepositions. "The facilitation of the integration of the data into the system" instead of "We integrated the data."

**Instead:** Turn nouns back into verbs. "We analyzed" not "our analysis of." "They decided" not "the decision was made." Active constructions with real verbs are harder for detectors to flag and easier for humans to read.

#### C33. No Colon-List Elision

**Rule:** Don't replace narrative explanation with "Topic: [bulleted list]" formatting. AI defaults to converting any multi-point discussion into a heading followed by a bulleted list, even when the points need connective tissue to make sense.

**Kill on sight:** Sections where every point is a standalone bullet with no transitional prose. Three or more consecutive colon-prefixed items that could be a paragraph.

**Instead:** Write it out. Explain the connections between points. A paragraph that says "The first problem is X, which leads to Y, and the combination makes Z worse" carries more information than three bullets that list X, Y, and Z independently.

#### C34. No Anthropomorphized Research

**Kill on sight:** Studies suggest, Research indicates, Data reveals, The literature demonstrates, Evidence points to, Science tells us, The findings highlight

**Instead:** Name the researchers or describe what was actually measured. "Reinhart found that LLM output has 15% more nouns" not "Research suggests a higher noun ratio." When research has no named author to cite, describe the methodology: "A 2025 analysis of 10,000 essays found..." not "Studies show..."

#### C35. Cross-Segment Stylistic Variation

**Rule:** Different sections of a long piece should not all read the same way. AI maintains consistent sentence structure, vocabulary level, and rhetorical patterns across sections. Human writers shift style as they move between topics: a technical section reads differently from a narrative section, which reads differently from an evaluative section.

**Instead:** Let the material drive the style. A section describing methodology can be dry and precise. A section discussing implications can be looser and more speculative. An anecdote should sound like a story, not like a report. If every section of a 3000-word piece could be shuffled without anyone noticing, the style is too uniform.

### Voice/Form constraints

#### C36. No Passive Voice Hiding or Subjectless Fragments

**Kill on sight:** Passive constructions that hide who did what ("the results are preserved automatically", "the decision was made", "the configuration is loaded"). Subjectless ad-copy fragments that drop the subject entirely ("No configuration file needed.", "Just works.", "Ready in seconds.").

**Problem:** LLMs default to passive voice and subjectless fragments because they sound technically clean. They actually obscure who acts and what does the work. Active voice with a real subject is harder for AI to produce and easier for humans to read.

**Before:**
> No configuration file needed. The results are preserved automatically.

**After:**
> You do not need a configuration file. The system preserves the results automatically.

**Instead:** Name the actor. "The system preserves" not "is preserved." "You configure" not "configuration is required." Some passive voice is legitimate (when the actor is unknown or genuinely irrelevant). The tell is the *frequency* and the *fragment-style brevity* of these constructions.

#### C37. No Hyphenated Word Pair Overuse (TIER 1)

**Kill on sight:** AI hyphenates common compound modifiers with perfect consistency. Watch for: third-party, cross-functional, client-facing, data-driven, decision-making, well-known, high-quality, real-time, long-term, end-to-end, top-tier, cutting-edge, future-proof, customer-facing, user-friendly, mission-critical.

**Problem:** Humans rarely hyphenate these uniformly. When a human does hyphenate, it's inconsistent ("data-driven" in one paragraph, "data driven" in the next). Perfect uniform hyphenation across 5+ compound modifiers in the same piece is one of the strongest 2026 AI tells. Less common or technical compounds (purpose-built, well-typed, copy-on-write) remain fine to hyphenate.

**Before:**
> The cross-functional team delivered a high-quality, data-driven report on our client-facing tools. Their decision-making process was well-known for being thorough and detail-oriented.

**After:**
> The cross functional team delivered a high quality, data driven report on our client facing tools. Their decision making process was known for being thorough and detail oriented.

**Instead:** Drop the hyphens from common compound modifiers. Keep them only where the meaning genuinely needs them (a "small-business owner" vs a "small business owner" — only one is grammatically ambiguous without the hyphen). Tier 1 because the visual uniformity is detector-friendly and reader-noticeable.

#### C38. No Signposting Announcements

**Kill on sight:** Let's dive in, let's explore, let's break this down, here's what you need to know, now let's look at, without further ado, in this section we will, before we begin, by the end of this you will

**Problem:** LLMs announce what they are about to do instead of doing it. This meta-commentary slows the writing down and gives it a tutorial-script feel. Distinct from C21 (chatbot artifacts like "I hope this helps") — signposting is pedagogical/instructional tone bleeding into prose.

**Before:**
> Let's dive into how caching works in Next.js. Here's what you need to know.

**After:**
> Next.js caches data at multiple layers: request memoization, the data cache, and the router cache.

**Instead:** Just start the topic. The reader knows you are about to explain something — they are reading the section. Strip every "let's", "here's what you need to know", and "in this section" sentence. The content underneath is almost always intact without the announcement.

#### C39. No Fragmented Headers

**Rule:** A heading should be followed by real content, not by a one-line paragraph that restates the heading.

**Kill on sight:** A header followed by a sentence that says the obvious thing about the topic, then a blank line, then the actual content begins. The restatement adds nothing — it is rhetorical warm-up.

**Before:**
> ## Performance
>
> Speed matters.
>
> When users hit a slow page, they leave.

**After:**
> ## Performance
>
> When users hit a slow page, they leave.

**Instead:** Cut the warm-up line. Start directly with the substantive content. If the header is "Performance", the reader does not need a sentence telling them performance is important — get to the point.

### Rhetorical staging and register constraints

C40 through C43 target one shared move: staging a reveal instead of making a claim. The writer builds a small frame — withheld knowledge, a suspenseful colon, a question they already answered, a closing aphorism — and the frame does the work the content should have done. Models produce these constantly because the shape is satisfying to generate and costs nothing to fill. C44 covers the register-level version of the same instinct.

#### C40. No Faux-Insight Setups

**Kill on sight:** What most people get wrong, Here's what nobody tells you, The part everyone misses, This is the part most people skip, What they don't tell you, The thing nobody talks about, Most people think X — they're wrong, Everyone focuses on X, but

**Problem:** These position the writer as the sole holder of a truth the reader's peers missed. The flattery is aimed at the writer, not the reader, and the claim that follows is almost always ordinary. The setup inflates the payload by implying suppressed knowledge that does not exist.

**Before:**
> The part everyone misses: distribution is the real moat.

**After:**
> Distribution is the moat.

**Instead:** Cut the setup and let the claim carry itself. A good claim does not need to be smuggled in as forbidden knowledge. If it collapses without the frame, it was not worth the sentence.

#### C41. No Colon Reveals

**Kill on sight:** A noun phrase, a colon, then a lowercase dramatic completion. "The detail that makes it work: a separate agent grades it." "The best part: it learns." "The catch: it only runs offline." "One problem: nobody asked for it."

**Problem:** The colon manufactures a beat of suspense the content has not earned. Distinct from C33 (colon-list elision, where narrative gets replaced by bullets) and C17 (`**Label:** content` bullet headers) — this one lives inside running prose and reads as copywriting cadence dropped into an essay.

**Before:**
> The detail that makes it work: a separate agent grades it.

**After:**
> A separate agent does the grading, which is what makes it work.

**Instead:** Rewrite as a plain sentence. Keep colons for lists, labels, and quotations. Where a colon is genuinely right, prefer sentence case after it unless grammar, a proper noun, a title, or code requires otherwise.

#### C42. No Rhetorical Setups or Self-Answered Questions

**Kill on sight:** What if I told you, Think about it:, Plot twist:, Here's a thought:, Ask yourself:, Sound familiar?, and any question posed only to be answered in the next sentence ("So what changed? Everything.").

**Problem:** The question is not a question. The writer already has the answer and is staging a beat of theatre to deliver it. Self-answered pairs are especially common in model output because they let the model produce structure in place of content.

**Before:**
> So why did adoption stall? The pricing.

**After:**
> Adoption stalled because of the pricing.

**Instead:** Make the statement. Keep a question only when you are genuinely leaving it open, or when you are asking the reader something you do not then answer for them.

#### C43. No Fake-Profound Kickers (TIER 1)

**Kill on sight:** A closing line that converts the piece's point into a metaphor, aphorism, or mic-drop. "The future was never the model. It was the eval." "Sometimes the simplest tool is the sharpest one." "And that, more than anything, is the real shift."

**Problem:** The kicker trades a concrete ending for a quotable one. It is the most reliably AI-shaped sentence in a piece, because models are trained toward satisfying closure and a final flourish always scores well. Distinct from C28 (generic positive endings), which is optimism without content; a kicker has cadence and manufactured depth. Tier 1 because it sits in the closing paragraph, which Pass 1 calibration already weights hardest, and because a single one flags the whole piece.

**Handling — delete, do not improve.** Do not rewrite the kicker into a better metaphor. Do not preserve its rhythm with a substitute line. Delete it outright, then end on the clearest concrete sentence already in the draft. If the piece genuinely lacks closure after the deletion, add a plain takeaway or a next action, never a flourish.

**Before:**
> Teams that measure their evals ship faster. In the end, what you measure is what you become.

**After:**
> Teams that measure their evals ship faster.

#### C44. No Empty Intensifiers

**Kill when empty:** just, simply, literally, truly, actually, honestly, really, basically, essentially, fundamentally, importantly, crucially, inherently, inevitably, clearly, obviously, undoubtedly, certainly

**Problem:** These get inserted to add weight and instead advertise that the sentence lacked it. "This is simply the fastest option" is weaker than "This is the fastest option." Stacked, they are a strong tell: "this is just fundamentally a better approach" carries three empty words and one real one.

**Keep when load-bearing.** Unlike most constraints here, this one is conditional by design. Keep the adverb when it carries genuine emphasis, real uncertainty, an actual contrast, or the writer's spoken rhythm.

- ✅ "I just wanted to check." (softening, spoken register)
- ✅ "It literally caught fire." (literal, not intensifying)
- ✅ "Honestly, I don't know." (real admission)
- ✅ "The API is fast. The SDK, obviously, is not." (contrast)
- ❌ "This is just fundamentally a better approach."
- ❌ "It's literally the best tool available."

**Test:** Delete the word and read the sentence. If nothing was lost, leave it deleted. If the meaning shifted or the writer's voice went flat, put it back. In preservation mode (Phase 2.5) the presumption flips toward keeping.

---

## Phase 2.5: Preservation mode (editing an existing draft)

Phases 1 through 3 assume you are composing. When the input is someone else's finished draft, the job inverts. The constraints still apply, but **the author's voice outranks them**. A clean rewrite that no longer sounds like the author is a failure even when every constraint passes.

**The rule: minimum effective edit.** Remove the AI patterns. Leave everything else alone. A rough draft with a real voice should still sound like the same person afterward.

**Protect these, even when a constraint flags them:**

| Surface | Why it survives |
|---|---|
| Hedges carrying real uncertainty — "I think", "maybe", "to be honest", "I'm not sure but" | C27 caps stacking, not hedging. C29 actively wants this variation. See the C27 carve-out. |
| Profanity, bluntness, strong opinions | Edge is voice. Do not upgrade it to professional register. |
| Digressions, asides, self-interruptions | C31 and Phase 3D want these. A real tangent outranks a tidy structure. |
| Fragments and long spoken sentences that are clear | C36 targets subjectless *ad-copy* fragments, not a writer's cadence. |
| Repeated vocabulary the author actually uses | C13 forbids synonym cycling; it does not license promoting "stuff" to "components". |
| Uneven polish across sections | C35 wants variation. Do not make every paragraph equally tidy. |
| Empty-looking intensifiers in dialogue or spoken-register prose | C44's presumption flips here. Delete only what is clearly dead. |

**Order of operations: restore specifics before sanding surface.** When editing existing text, the deepest failure is usually not that the prose is fancy — it is that concrete detail (names, numbers, dates, mechanisms) was laundered into abstraction somewhere upstream. Run the Phase 3C specificity pass first, then the pattern passes. Combine this with the Pass 1 calibration: thin clusters, do not shave every instance.

**Output contract — this is the one place Phase 5 is suspended.** When the user handed you their draft, return the edited text **plus a short "What changed" list**. They need to be able to reject an individual edit, which requires seeing it. Keep the list short and specific: what you removed, and why in a few words. Phase 5's no-meta-commentary rule governs composition, not editing.

**Detect-only requests.** If the user asks whether a piece reads as AI *without* asking for a rewrite, do exactly that and stop:

- Name each constraint that fires, with its C-number.
- Quote the line it fired on.
- Give the fix in a few words.
- Do **not** rewrite the draft.
- Do **not** score it, rate it, or give a percentage.
- Do **not** estimate whether a model wrote it. Detectors guess; a named pattern is evidence the user can check themselves. That distinction is the whole value of the report.

Offer the rewrite afterward.

---

## Phase 3: Voice injection (during and after composition)

Avoiding patterns produces clean text. Clean text is not the same as good text. This phase adds the human element.

### 3A. Sentence rhythm variation

Read the draft and check sentence lengths. If three consecutive sentences are within 5 words of each other in length, rewrite one. A piece with all 15-word sentences is as suspicious as one with all 40-word sentences.

Pattern to aim for: short (5-10), medium (15-20), long (25-35), short, medium. Not rigidly, just not monotone.

### 3B. Opinion insertion

For every section longer than 3 paragraphs, check: does the author have a visible opinion? If the whole section reads like neutral reporting, find one place to react.

Reactions don't need to be strong. "This surprised us" or "We didn't expect that to matter" or "Frankly, this is the part that worries me." Any signal that a thinking person is behind the text.

### 3C. Specificity pass

Scan for abstract claims. Every time you find one, try to attach a number, a name, a date, or a concrete example.

| Abstract | Specific |
|----------|----------|
| significant improvement | 55% faster in our tests |
| widely adopted | used by 12 of the 20 largest banks |
| experts agree | three independent reviews reached the same conclusion |
| many users reported | 340 bug reports in the first week |

If you can't make it specific, consider whether you actually know enough to make the claim.

### 3D. Imperfection allowance

Perfect structure signals algorithm. Allow yourself:
- One tangent or aside per major section
- One sentence that starts with "But" or "And"
- One place where you acknowledge you're not sure
- One observation that's slightly off-topic but interesting

Don't force these. But don't sterilize them out either.

---

## Phase 4: Verification (after draft is complete)

Four passes, run in order. Pass 1 and Pass 2 are mechanical (grep + checklist). Pass 3 is introspective (ask yourself the question). Pass 4 is sensory (read aloud). Each pass targets a different failure mode.

### Pass 1: Pattern scan (automated)

Run these grep patterns against the draft. Any hit requires a rewrite of that sentence.

**High-confidence AI tells (rewrite on any match):**

```
# Content inflation (C1)
\b(testament|pivotal|landscape|tapestry|indelible|enduring legacy)\b

# AI vocabulary (C9)  -- includes "actually" added in v2.1.0
\b(Actually|Additionally|delve|intricacies|interplay|underscore|showcase|fostering|garner|comprehensive|exhibited|multifaceted|notably|particularly|meticulous|swift)\b

# Promotional + persuasive authority tropes (C4)
\b(vibrant|groundbreaking|breathtaking|nestled|renowned|stunning|must-visit)\b
(the real question is|at its core|in reality|what really matters|fundamentally|the deeper issue|the heart of the matter|in the realm of)

# Copula avoidance (C10)
\b(serves as|stands as|boasts a|features a)\b

# Chatbot artifacts (C21)
(I hope this helps|Of course!|Certainly!|Would you like|let me know|here is a)

# Sycophancy (C23)
(Great question|excellent point|fascinating|You're absolutely right)

# Participial filler (C3)
\b(highlighting|underscoring|emphasizing|symbolizing|showcasing|encompassing)\b
(,\s*ensuring|,\s*reflecting|,\s*contributing to|,\s*fostering|,\s*aligning)

# Hedging stacks (C27)
(could potentially|might possibly|it could be argued|it is worth noting)

# Generic endings (C28)
(future looks bright|exciting times|journey toward|step in the right direction)

# Chatbot tracking artifacts (C24)
(utm_source=|citeturn\d|contentReference|oaicite|oai_citation|grok_card|attached_file|INSERT_SOURCE|attributableIndex)

# Hyphenated word pair overuse (C37) -- TIER 1: count uniform-hyphen instances
\b(third-party|cross-functional|client-facing|customer-facing|data-driven|decision-making|well-known|high-quality|real-time|long-term|end-to-end|top-tier|cutting-edge|future-proof|user-friendly|mission-critical)\b

# Signposting announcements (C38)
(Let's dive in|let's explore|let's break this down|here's what you need to know|now let's look at|without further ado|in this section we will|before we begin|by the end of this you will)

# Subjectless ad-copy fragments (C36)
^(No \w+ needed|Just works|Ready in seconds|Built for|Designed for)\.?$

# RAG disclaimers (C22)
(in the provided sources|in the available sources|not widely documented|not widely disclosed|maintains a low profile|keeps personal details private)

# Filler phrases - historical but still caught (C26)
(it's important to note|it's crucial to note|it's critical to note|worth noting that|it bears mentioning|navigating the complexities)

# Anthropomorphized research (C34)
(studies suggest|research indicates|data reveals|the literature demonstrates|evidence points to|science tells us|the findings highlight)

# Promotional phrases (C4 expanded)
(at its core|in the realm of|shed light on|a myriad of)

# Nominalization chains (C32)
(the implementation of|the utilization of|the facilitation of|the integration of)

# Em dashes (C15) -- TIER 1: most visible structural tell in 2026
—
 --

# Faux-insight setups (C40)
(what most people get wrong|nobody tells you|the part everyone misses|most people skip|what they don't tell you|the thing nobody talks about)

# Rhetorical setups (C42)
(what if I told you|think about it:|plot twist:|here's a thought:|ask yourself:|sound familiar\?)

# Fake-profound kickers (C43) -- TIER 1: check the FINAL paragraph specifically
(in the end,|at the end of it all|and that,? more than anything|what you measure is what you|the real .{0,20} was never)

# Hype/marketing register (C9 v2.3.0)
\b(empower|supercharge|elevate|embark|transformative|paramount|ever-evolving|game.?chang(er|ing)|unleash|revolutioniz|seamless|effortless|next-level)\b
(this is huge|this changes everything|let that sink in)

# Filler openers (C26 v2.3.0)
(when it comes to|in terms of|with regard to|with respect to|in today's world|in the age of|in the world of|the reality is|the truth is|going forward|in this article|in this post)
```

**Positional note for C43.** Kickers only appear in closing position. Do not grep the whole draft for them — read the final paragraph of the piece and of each major section, and ask whether the last sentence states a fact or performs a flourish. The regex above catches common phrasings; the pattern itself is structural and the regex will miss most instances.

**Context-gate C41 and C44.** Neither has a usable regex. C41 (colon reveals) requires distinguishing a dramatic reveal from a legitimate list or label — grep every `: ` and you will drown in false positives. C44 (empty intensifiers) is conditional by design; a raw match tells you nothing about whether the word is load-bearing. Catch both by reading, in Pass 2.

**Medium-confidence (review, may be legitimate):**

```
# Rule of three (three comma-separated abstract nouns) (C12)
\b\w+tion,\s+\w+tion,\s+and\s+\w+tion\b

# Negative parallelism (C11)
(not just|not only|not merely).{0,30}(but also|it's about|it's a)

# Tailing negation fragments (C11)
,\s*(no guessing|no wasted motion|no friction|no surprises|no nonsense)\.?$

# Passive voice hiding (C36) -- common subjectless or actor-hiding constructions
\b(is preserved|are preserved|is loaded|are loaded|is configured|are configured)\s+(automatically|by default)\b

# False ranges (C14)
from\s+.{5,30}\s+to\s+.{5,30},\s+from\s+

# Curly quotes (C25)
[\u201C\u201D\u2018\u2019]

# Source quantity inflation (C5)
\b(several (sources|publications|studies|reports))\b

# Notability puffing (C2)
(active social media presence|profiled in|media outlets)
```

### Pass 1 calibration: grade by density, then thin — don't shave

A raw grep hit is a flag, not an automatic delete. Two rules turn the match list into proportional action.

**Grade by density, not mere presence.** The tell is co-occurrence, not any single word (see the C9 note; Kobak et al. 2024). Score each pattern by frequency per 1000 words and by position, then rewrite worst-first:
- **HIGH** — any Tier-1 pattern; OR any pattern at >1 per 1000 words; OR ≥3 tells clustered in one paragraph; OR any tell in the opening/closing paragraph or an abstract/intro (openings are read first and weighted hardest).
- **MED** — ~1 per 2000 words; OR 2 tells in one paragraph.
- **LOW** — isolated, rare, outside openings. Legitimate in some contexts (Tier 3) — flag, don't reflexively rewrite.

**Thin the cluster, don't shave every word.** Over-correction is its own failure mode: strip *every* instance of *every* pattern and the prose collapses into a flat, sanitized "regression-to-the-mean" voice that reads just as artificial as the slop you started from. When a paragraph carries six tells, removing three usually restores a human cadence; removing all six produces a different, equally-detectable flatness. Leave enough variety — one em dash within the C15 cap, an occasional real rule-of-three, a single "however" — that the result reads like a specific person, not a scrubbed average. This bites hardest in **review/rewrite mode** (editing existing text rather than composing fresh): there the deepest diagnostic is not "does this sound fancy?" but "were concrete specifics — names, numbers, dates — available and laundered into generic abstraction?" Restore the specifics (Phase 3C) before you sand the surface.

### Pass 2: Structural audit

Check these by reading, not by grep:

1. **Sentence length variance**: Sample 10 consecutive sentences. Measure word counts. Standard deviation should be > 5. If it's < 3, you have monotone cadence.

2. **Paragraph opening words**: List the first word of every paragraph. If more than two start with "The" or more than two start with the same word, vary them.

3. **Section structure**: If every section follows the same pattern (claim → evidence → interpretation), break at least one. Put the evidence first sometimes. Start with the interpretation. Vary the skeleton.

4. **Opinion presence**: At least one first-person statement per 500 words of analytical content. Zero first-person in a 2000-word analysis is a red flag.

5. **Concrete detail ratio**: Count abstract claims vs. specific details (numbers, names, dates, measurements). Aim for at least 1 specific detail per 3 sentences.

6. **Table justification**: For every table in the draft, ask: does this have at least 3 rows and 2 columns? Could the data be stated in a sentence instead? If yes, convert to prose. Small unnecessary tables are a common AI tell.

7. **Citation integrity**: For every source cited, verify you actually know the author/year/publication. If any citation feels like something you generated rather than something you retrieved, remove it or replace with an honest hedge.

8. **Confidence variation (C29)**: Read through the draft and check whether every claim is stated with equal certainty. Mark places where you're less sure and add appropriate hedging there. If no hedges exist in 500+ words of analytical content, the confidence is too uniform.

9. **Cross-segment style (C35)**: Compare the first paragraph of each major section. If they all follow the same rhetorical pattern (e.g., all start with a general claim, all use similar sentence lengths, all have the same density of technical terms), vary at least two sections.

10. **Noun-verb check (C32)**: Pick any paragraph. Count nouns and verbs. If nouns outnumber verbs by more than 3:1, rewrite nominalized phrases into active constructions.

### Pass 3: Self-audit (introspective)

After Pass 1 and Pass 2, ask yourself the question explicitly:

> "What makes the below so obviously AI generated?"

Then answer in 2-5 brief bullets, naming the residual tells you can still see. Be specific: not "tone is off" but "the rhythm is too tidy, the conclusion still slogan-y, the named example reads as plausible-but-fictional".

Then revise once more, with the prompt:

> "Now make it not obviously AI generated."

This pass catches what Pass 1 (regex) and Pass 2 (structural) cannot — the holistic "this still smells AI" signal that comes from rhythm, voice, and trust calibration. It is cheap (one more scan) and high-value: most pieces still have one or two tells after Pass 1+2 that only surface when you ask the question directly.

### Pass 4: Read-aloud test

Read the opening paragraph and the closing paragraph aloud (mentally). Check:

- Do any phrases feel unnatural to say out loud? Rewrite them.
- Does the opening sound like a human starting a conversation or a machine outputting a summary?
- Does the ending feel like a person finishing a thought or an algorithm wrapping up?
- Would you be comfortable putting your name on this? If something makes you wince, fix it.

---

## Phase 5: Final output

After verification, produce the text. No meta-commentary about the process unless the user asks for it.

If the user requested the piece in a file, use Write/Edit to save it. If they requested it in conversation, output it directly.

**Do not:**
- Mention that you used this skill
- Add disclaimers about the humanization process
- Offer to "expand on any section"
- End with "Let me know if you'd like any changes"

**Do:**
- Output the text as if a human wrote it
- If verification caught problems, fix them silently
- If you have genuine uncertainty about tone or scope, ask the user before writing (Phase 1), not after

**Exception — preservation mode.** This section governs composition. When you edited a draft the user handed you, Phase 2.5 applies instead: return the edited text plus a short "What changed" list, so the user can reject an individual edit.

---

## Quick reference: the 44 constraints

| # | Constraint | Category | Trigger |
|---|-----------|----------|---------|
| C1 | No significance inflation | Content | testament, pivotal, crucial, vital |
| C2 | No notability puffing | Content | media outlets, social media presence |
| C3 | No participial filler | Content | -ing phrases tacked onto sentences |
| C4 | No promotional tone or persuasive authority tropes | Content | vibrant, nestled, the real question is, fundamentally, at its core |
| C5 | No vague attributions / source inflation | Content | Experts argue, several sources |
| C6 | No formulaic sections | Content | Despite challenges, In conclusion |
| C7 | No title-as-proper-noun openings | Content | "X is a [category] that..." |
| C8 | No hallucinated citations | Content | Invented DOIs, ISBNs, sources |
| C9 | No AI vocabulary | Language | Actually, Additionally, comprehensive, notably |
| C10 | No copula avoidance | Language | serves as, stands as, boasts |
| C11 | No negative parallelisms or tailing negations | Language | Not just...but..., "no guessing" tacked on |
| C12 | No forced rule-of-three | Language | Three abstract nouns in sequence |
| C13 | No synonym cycling | Language | Rotating referents for same entity |
| C14 | No false ranges | Language | from X to Y, from A to B |
| C15 | Em dash discipline (TIER 1) | Style | Kill on sight. Max 1 per 500 words. Most visible structural tell. |
| C16 | Boldface restraint | Style | Only structural headers |
| C17 | No inline-header lists | Style | `**Label:** content` bullets |
| C18 | Sentence case headings | Style | Title Case Headings |
| C19 | No emojis | Style | Unless user requests |
| C20 | No unnecessary tables | Style | Small tables better as prose |
| C21 | No chatbot artifacts | Communication | I hope this helps, Certainly! |
| C22 | No cutoff/RAG disclaimers | Communication | as of, in the provided sources |
| C23 | No sycophancy | Communication | Great question!, excellent point |
| C24 | No chatbot tracking artifacts | Communication | utm_source, oaicite, citeturn |
| C25 | Straight quotes | Communication | Curly quotes |
| C26 | No filler phrases | Filler/Hedging | In order to, important to note |
| C27 | No excessive hedging | Filler/Hedging | could potentially possibly |
| C28 | No generic endings | Filler/Hedging | future looks bright, exciting times |
| C29 | No uniform confidence | Epistemic | Equal certainty on all claims |
| C30 | No view from nowhere | Epistemic | Omniscient disembodied narrator |
| C31 | Sentence burstiness | Structural | Uniform predictability across sentences |
| C32 | Noun-verb ratio | Structural | Nominalization chains, passive nouns |
| C33 | No colon-list elision | Structural | Narrative replaced by bulleted lists |
| C34 | No anthropomorphized research | Structural | Studies suggest, research indicates |
| C35 | Cross-segment variation | Structural | All sections read identically |
| C36 | No passive voice hiding / subjectless fragments | Voice/Form | "is preserved automatically", "No config needed." |
| C37 | No hyphenated word pair overuse (TIER 1) | Voice/Form | third-party, cross-functional, data-driven uniformly hyphenated |
| C38 | No signposting announcements | Voice/Form | Let's dive in, here's what you need to know |
| C39 | No fragmented headers | Voice/Form | Header → one-line restatement → real content |
| C40 | No faux-insight setups | Rhetorical staging | What nobody tells you, the part everyone misses |
| C41 | No colon reveals | Rhetorical staging | "The best part: it learns." |
| C42 | No rhetorical setups / self-answered questions | Rhetorical staging | What if I told you, Plot twist:, "So why? Pricing." |
| C43 | No fake-profound kickers (TIER 1) | Rhetorical staging | Closing metaphor or aphorism. Delete, don't improve. |
| C44 | No empty intensifiers | Register | just, simply, literally, truly, obviously (when empty) |

---

## Ineffective indicators (do not flag these)

Not every imperfection is an AI tell. The following are NOT reliable signs of AI-generated text and should not trigger rewrites:

- **Perfect grammar** alone. Humans can write grammatically correct prose.
- **Mixing casual and formal registers.** Many human writers shift register naturally.
- **"Bland" or "robotic" prose.** Some humans write blandly. Blandness is not evidence.
- **Unusual or academic vocabulary.** Domain experts use domain words. A physicist writing "eigenvalue" is not an AI tell.
- **Letter-like or epistolary structure** in isolation. Humans write letters.
- **Use of conjunctions** (Additionally, Furthermore, Moreover) in isolation. One "Additionally" is not a tell; five in the same piece is.

These are noted as ineffective because over-flagging them produces false positives and wastes editing effort on non-issues. Focus on the 44 constraints above, which target patterns that actually distinguish AI output from human writing at scale.

---

## Reference

Primary sources:
- [blader/humanizer](https://github.com/blader/humanizer) v2.5.1 (MIT, Siqi Chen). Upstream 29-pattern catalog. C36-C39 ported directly; C9 ("actually") and C11 (tailing negations) augmented from upstream PRs #80, #79, #72, #42.
- [petergyang/no-ai-slop](https://github.com/petergyang/no-ai-slop) (MIT, Peter Yang), commit `61c21c3`, July 2026. An editing-mode skill whose organizing principle is voice preservation. C40-C43 derived from its pattern catalog (faux-insight setups, colon reveals, rhetorical setups, fake-profound kickers), C44 from its often-empty-adverb list, and the C9/C26 hype-register extensions from its banned-word and filler-phrase lists. Phase 2.5 preservation mode and the detect-only doctrine (name the pattern, quote the line, never score or claim AI authorship) are adapted from its editing principles and eval checks.
- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (April 2026 revision), maintained by WikiProject AI Cleanup. Covers all 8 major categories. Platform-specific patterns (broken wikitext, hallucinated Wikipedia categories/templates, AFC submission statements) omitted as not applicable to general writing.
- Kobak et al. (2024): Excess word frequency analysis across LLM output vs. human baselines. 329 words with statistically significant overuse; top 10 integrated into C9.
- Reinhart (PNAS 2025): Noun-to-verb ratio distortion in LLM output. Basis for C32.
- Tripto et al. (EMNLP 2025): Cross-segment stylistic uniformity and flow-dependent features as detection signals. Basis for C29, C35.
- DivEye (2025): Burstiness deficit (low perplexity variance) in LLM text. Basis for C31.
- Yakura et al. (2024): Cultural feedback loop words. RLHF-amplified vocabulary integrated into C9.
- lmmx AI Tells Rubric: Community-maintained catalog of 30+ epistemic tells. Basis for C30, C33, C34.
- Dentella & Wang (EMNLP 2025): Register rigidity in LLM output. Supporting evidence for C35.

Adapted from detection/editing frameworks into proactive composition constraints with automated verification.
