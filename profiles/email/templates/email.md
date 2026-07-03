# Email writing system

Standing instructions for how I write emails, and the workflow for drafting them with Claude. The point of this system is to kill the blank-page block: I open a session, say what the email needs to do, and we draft and iterate until it's right. I should never start an email from nothing again.

This file starts as a skeleton and calibrates itself through use: the `/email` skill logs observations after every email, promotes repeated ones into standing rules, and audits every draft against what it has learned. Sections marked FILL ME benefit from an hour of upfront seeding; everything else can start empty.

## How to use this

1. **`/email <task>`**: fastest. Type the command with a one-line task (e.g. `/email reschedule Thursday's advisor meeting to next week`). Claude loads this guide, asks only what it can't infer, drafts, and we iterate in chat. Save the final version to the drafts folder if it's worth keeping.
2. **Open this note** and talk to Claude with it in context. Same thing, manual.

The iteration loop: Claude drafts, I react in plain language ("too formal", "cut the second paragraph", "I also need to mention X"), Claude revises, repeat until I say it's done. I do not need to know what's wrong in writing terms; reacting is enough.

## Core voice (my default in every email)

<!-- FILL ME: 4-8 bullets describing your default register. Be honest, not aspirational; the system drafts from this. Prompts to react to:
- Warm or reserved openers? ("Hope you're doing well!" vs straight to business)
- Direct asks or softened requests? ("Send me X" vs "When you have a chance, could you...")
- Do you hedge on purpose? Which hedges are your voice vs filler?
- Sentence length, formality, contractions?
- Anything you never do (emojis, exclamation marks, "Best regards")?
Two rules worth keeping for almost everyone: -->

- Clear underneath whatever politeness I use: the reader should finish the email knowing exactly what I'm asking and what happens next.
- One idea per sentence; easy to read. No marketing voice, no hype words.

## The four-part skeleton (what every email needs)

When I don't know what to include, fill these four slots. Drop any that don't apply:

1. **Why I'm writing:** the context/trigger, one sentence (often paired with or following the opener).
2. **The ask:** clear, not buried three paragraphs deep. The reader shouldn't have to hunt for what I need.
3. **What they need to act:** the details, dates, links, or constraints required to say yes.
4. **The next step:** who does what by when, left open enough that they can adjust.

If an email has no ask, the close is just a clear statement of what happens next (or "no reply needed").

## Tone / formality ladder

Pick the rung by recipient, not by mood. The rung sets how formal the *wording* is; it does not decide whether I'm friendly.

| Rung | Recipient | Greeting | Sign-off | Notes |
|------|-----------|----------|----------|-------|
| 1 (Formal) | Cold professional contact, anyone senior I've not met | "Dear ___," | "Best regards," | Full sentences, careful wording. |
| 2 (Professional) | Managers, advisors, collaborators, established work contacts | "Hi ___," | "Best," | Contractions fine. Warm opener where there's a relationship. |
| 3 (Friendly-pro) | Customers, suppliers, peers I know | "Hi ___," | "Thanks so much," | Warm and personable, still purposeful. |
| 4 (Casual) | People I know well, quick logistics | "Hey ___," | first name only | Brief, can skip preamble. |

<!-- Adjust greetings/sign-offs to what you actually use. The skill logs mismatches over time. -->

## Conciseness rules

- Concise means cutting redundant backstory and repeated points, not courtesy.
- If a sentence doesn't change what the reader does or knows (and isn't doing courtesy work), cut it.
- One ask per email when possible. Two max. More than that, use a numbered list.
- Default target: under ~150 words for a routine email. If it's longer, ask whether it needs to be.

## Things I want to stop doing (anti-patterns)

<!-- FILL ME over time: your own tells. The skill will propose additions as it observes your edits. -->

- Over-explaining the backstory before the ask gets through.
- Saying the same point twice in different words.

## Email-specific tells (scrub list)

Words and phrasings that stand out against my tone. The `/email` skill audits every draft against this list before showing me anything. Grows from Observed patterns; the dated log below keeps the history.

- Em dashes and en dashes: a strong AI tell in email; use a period, comma, or parentheses.
<!-- The skill adds entries here as patterns get promoted. Seed it with any phrases you already know you hate ("per my last email", "circle back", "touch base"...). -->

## Phrasing bank

<!-- FILL ME through use: your confirmed go-to phrasings, chosen from real drafts. The skill proposes additions when you keep a phrasing repeatedly. Categories to grow: -->

**Openers (warm):**

**Asks:**

**Closers / sign-offs:**

**Apologies / flagging a change of plans:**

**Scheduling and flexibility:**

**Gratitude:**

## Email types and tone (grows as I write)

A map from the kind of email to the tone that fit it, built from real emails I've sent. When starting a new email, find the closest type here first and start from that tone. Each entry points to a saved draft as a worked example.

<!-- The skill adds entries as you write: type, recipient relationship, the tone that worked, link to the draft. -->

## Recipients (recurring)

One entry per person I email repeatedly: rung, register, standing context, and prior drafts. The skill checks here first when drafting, and checks the linked drafts to avoid reusing exact phrases with the same person. For a recipient with no entry, it falls back to the closest type in the map above.

<!-- Entry shape:
### Name (relationship)
- Rung N. Greeting "...", sign-off "...".
- Register: ...
- Standing context: ...
- Prior drafts: links
-->

## Observed patterns (auto-updated as we write)

Claude appends short, dated notes here after emails we draft together: recurring phrasings I reach for, openers/sign-offs I keep, things I consistently cut or rephrase. Over time this is what tunes the skill to my real voice. Keep entries terse; prefer exact before/after phrase pairs.

Lifecycle: a pattern's second occurrence triggers a promotion proposal (to Core voice, the Phrasing bank, the scrub list, or a Recipients entry). Promoted bullets stay here as history, suffixed "(promoted to X, YYYY-MM-DD)". Contradictions: newest wins, old entry suffixed "(superseded YYYY-MM-DD)". Past ~25 unpromoted entries, distill instead of appending.

## Good examples

Real emails I was happy with. Link plus one line on why it worked; the draft file holds the full text (single source of truth; no second copies here).

<!-- HIGHEST-VALUE SEEDING: paste or link 2-3 real emails you liked. Real examples outrank every written rule above. -->
