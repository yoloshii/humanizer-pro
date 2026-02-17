---
name: humanizer-pro
description: |
  Generates human-sounding text from scratch using 35 anti-AI-pattern constraints applied during composition. Use when writing reports, analyses, articles, feedback documents, essays, documentation, blog posts, or any substantial text where AI detection is a concern. Also use when user says "write this like a human," "make it sound natural," "no AI slop," or "use humanizer." Handles voice calibration, constraint-driven composition, rhythm variation, opinion injection, specificity passes, and three-pass automated verification (pattern scan, structural audit, read-aloud test). Aligned with Wikipedia:Signs of AI writing (February 2026 revision) and peer-reviewed stylometric research (2024-2026).
allowed-tools: "Read Write Edit Grep AskUserQuestion"
metadata:
  version: 2.0.0
---

# Humanizer Pro: Write like a human from the start

## Quick start

1. Determine voice profile (register, perspective, stance, audience)
2. Load 35 anti-pattern constraints as active composition rules
3. Write the piece with constraints applied per-sentence
4. Inject voice: vary rhythm, insert opinions, add specifics, allow imperfection
5. Run three-pass verification: pattern scan (Grep), structural audit, read-aloud test
6. Output clean text with no meta-commentary

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

These 35 constraints are active during composition. They are not a checklist to run afterward. They shape every sentence as you write it.

Memorize the constraint categories:
- **Content (1-8)**: What you say and how you source it
- **Language (9-14)**: How you construct sentences
- **Style (15-20)**: How it looks on the page
- **Communication (21-25)**: Chatbot artifacts and paste residue
- **Filler/Hedging (26-28)**: Verbal padding
- **Epistemic/Structural (29-35)**: How you think and organize on the page

Not all constraints carry equal weight. During composition, allocate attention by priority:

- **Tier 1 (instant tells, always rewrite)**: C1, C9, C21, C23, C24, C26, C34. A single hit from any of these is enough to flag a piece. These are the patterns detectors and human reviewers catch first.
- **Tier 2 (strong signals, rewrite on sight)**: C3, C4, C10, C12, C28, C32, C33. One instance may pass; two in the same piece is a pattern.
- **Tier 3 (contextual, check before rewriting)**: C2, C5, C7, C8, C11, C13, C14, C15, C20, C22, C25, C27. These are legitimate in some contexts. Flag them, but don't blindly rewrite.
- **Tier 4 (holistic, assess in structural audit)**: C6, C16, C17, C18, C19, C29, C30, C31, C35. These can't be caught per-sentence. Evaluate at the draft level in Pass 2.

**Instruction-layer note:** These instructions use structured lists, bold labels, tables, colon-prefixed items, and uniformly authoritative tone. This formatting is optimized for LLM instruction parsing. Do not replicate it in output. The constraints below govern what you write for the user, not how these instructions are formatted.

### 1C. Prime the rhythm

Write a throwaway opening sentence that is deliberately short. Under 8 words. This anchors your rhythm. If your first sentence is 30 words long, the whole piece drifts toward uniform long sentences.

---

## Phase 2: Composition (active constraints)

Write the piece with all 35 constraints loaded. Each constraint below includes its trigger patterns and what to do instead.

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

#### C4. No Promotional Tone

**Kill on sight:** boasts a, vibrant, rich (figurative), profound, enhancing its, exemplifies, commitment to, natural beauty, nestled, in the heart of, groundbreaking (figurative), renowned, breathtaking, must-visit, stunning, at its core, in the realm of, shed light on, a myriad of

**Instead:** Describe concretely. Dimensions, dates, names, numbers. "A 200-seat restaurant that opened in 2019" not "a vibrant dining destination."

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

**Kill on sight:** Additionally, align with, comprehensive, crucial, delve, emphasizing, enduring, enhance, exhibited, fostering, garner, highlight (verb), insights, interplay, intricate/intricacies, key (adjective), landscape (abstract), meticulous, multifaceted, notably, particularly, pivotal, realm, showcase, swift, tapestry (abstract), testament, underscore (verb), valuable, vibrant, within (when "in" works)

**Instead:** Use the plainest word that works. "Important" not "crucial." "Show" not "showcase." "Also" not "Additionally." "Thorough" not "comprehensive." "Showed" not "exhibited." Most of these words have simple equivalents.

**Note:** "delve" dropped off sharply in 2025 LLM output but remains a strong historical tell. Words like "comprehensive," "notably," "particularly," "within," and "multifaceted" were identified by Kobak et al. (2024) as having the highest excess frequency in LLM output vs. human baselines. Co-occurrence is the real signal: one or two of these words may be coincidence; five in the same piece is not.

#### C10. No Copula Avoidance

**Kill on sight:** serves as, stands as, marks, represents [a], boasts, features, offers [a]

**Instead:** Write "is" or "has." Gallery 825 is the exhibition space. The building has four rooms. Stop flinching from simple verbs.

#### C11. No Negative Parallelisms

**Kill on sight:** Not only...but..., It's not just about..., it's..., It's not merely...it's..., no..., no..., just...

**Instead:** State the positive claim directly. "The beat adds aggression" not "It's not just about the beat, it's about the aggression."

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

**Rule:** Maximum one em dash (or double-hyphen substitute) per 500 words. Zero is better. If you catch yourself reaching for an em dash or typing ` -- ` as a parenthetical separator, use a comma, a period, or parentheses. Note: some newer models (2025+) use em dashes less, but the pattern remains a tell in aggregate. Double hyphens used as em dash substitutes count toward the same limit; double hyphens in CLI flags (--enable-features) and code do not.

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

**Note:** "It's important to note" and "worth noting" were among the strongest AI tells in 2022-2024. They appear less often in 2025+ model output but remain worth catching.

#### C27. No Excessive Hedging

**Rule:** One hedge per claim maximum. "This may affect outcomes" is fine. "This could potentially possibly be argued to have some effect" is four hedges on one verb.

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

Three automated passes, run in order. Each pass targets a different failure mode.

### Pass 1: Pattern scan (automated)

Run these grep patterns against the draft. Any hit requires a rewrite of that sentence.

**High-confidence AI tells (rewrite on any match):**

```
# Content inflation (C1)
\b(testament|pivotal|landscape|tapestry|indelible|enduring legacy)\b

# AI vocabulary (C9)
\b(Additionally|delve|intricacies|interplay|underscore|showcase|fostering|garner|comprehensive|exhibited|multifaceted|notably|particularly|meticulous|swift)\b

# Promotional (C4)
\b(vibrant|groundbreaking|breathtaking|nestled|renowned|stunning|must-visit)\b

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
```

**Medium-confidence (review, may be legitimate):**

```
# Em dash density (C15) -- includes double-hyphen substitutes
—
 --

# Rule of three (three comma-separated abstract nouns) (C12)
\b\w+tion,\s+\w+tion,\s+and\s+\w+tion\b

# Negative parallelism (C11)
(not just|not only|not merely).{0,30}(but also|it's about|it's a)

# False ranges (C14)
from\s+.{5,30}\s+to\s+.{5,30},\s+from\s+

# Curly quotes (C25)
[\u201C\u201D\u2018\u2019]

# Source quantity inflation (C5)
\b(several (sources|publications|studies|reports))\b

# Notability puffing (C2)
(active social media presence|profiled in|media outlets)
```

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

### Pass 3: Read-aloud test

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

---

## Quick reference: the 35 constraints

| # | Constraint | Category | Trigger |
|---|-----------|----------|---------|
| C1 | No significance inflation | Content | testament, pivotal, crucial, vital |
| C2 | No notability puffing | Content | media outlets, social media presence |
| C3 | No participial filler | Content | -ing phrases tacked onto sentences |
| C4 | No promotional tone | Content | vibrant, nestled, at its core, myriad |
| C5 | No vague attributions / source inflation | Content | Experts argue, several sources |
| C6 | No formulaic sections | Content | Despite challenges, In conclusion |
| C7 | No title-as-proper-noun openings | Content | "X is a [category] that..." |
| C8 | No hallucinated citations | Content | Invented DOIs, ISBNs, sources |
| C9 | No AI vocabulary | Language | Additionally, comprehensive, notably |
| C10 | No copula avoidance | Language | serves as, stands as, boasts |
| C11 | No negative parallelisms | Language | Not just...but..., Not merely...it's |
| C12 | No forced rule-of-three | Language | Three abstract nouns in sequence |
| C13 | No synonym cycling | Language | Rotating referents for same entity |
| C14 | No false ranges | Language | from X to Y, from A to B |
| C15 | Em dash discipline | Style | Max 1 per 500 words |
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

---

## Ineffective indicators (do not flag these)

Not every imperfection is an AI tell. The following are NOT reliable signs of AI-generated text and should not trigger rewrites:

- **Perfect grammar** alone. Humans can write grammatically correct prose.
- **Mixing casual and formal registers.** Many human writers shift register naturally.
- **"Bland" or "robotic" prose.** Some humans write blandly. Blandness is not evidence.
- **Unusual or academic vocabulary.** Domain experts use domain words. A physicist writing "eigenvalue" is not an AI tell.
- **Letter-like or epistolary structure** in isolation. Humans write letters.
- **Use of conjunctions** (Additionally, Furthermore, Moreover) in isolation. One "Additionally" is not a tell; five in the same piece is.

These are noted as ineffective because over-flagging them produces false positives and wastes editing effort on non-issues. Focus on the 35 constraints above, which target patterns that actually distinguish AI output from human writing at scale.

---

## Reference

Primary sources:
- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (February 2026 revision), maintained by WikiProject AI Cleanup. Covers all 8 major categories. Platform-specific patterns (broken wikitext, hallucinated Wikipedia categories/templates, AFC submission statements) omitted as not applicable to general writing.
- Kobak et al. (2024): Excess word frequency analysis across LLM output vs. human baselines. 329 words with statistically significant overuse; top 10 integrated into C9.
- Reinhart (PNAS 2025): Noun-to-verb ratio distortion in LLM output. Basis for C32.
- Tripto et al. (EMNLP 2025): Cross-segment stylistic uniformity and flow-dependent features as detection signals. Basis for C29, C35.
- DivEye (2025): Burstiness deficit (low perplexity variance) in LLM text. Basis for C31.
- Yakura et al. (2024): Cultural feedback loop words. RLHF-amplified vocabulary integrated into C9.
- lmmx AI Tells Rubric: Community-maintained catalog of 30+ epistemic tells. Basis for C30, C33, C34.
- Dentella & Wang (EMNLP 2025): Register rigidity in LLM output. Supporting evidence for C35.

Adapted from detection/editing frameworks into proactive composition constraints with automated verification.
