# The learning loop

The protocol that makes a voice profile improve itself. The email skill implements it; future profiles (papers, posts) reuse it unchanged.

## The two layers

- **Engine**: the skill instructions. How to draft, iterate, observe, promote, and audit. Generic; shared; versioned in this repo.
- **Data**: one person's voice. Style guide, phrasing bank, recipient profiles, drafts, observed-patterns log. Private; grows locally; never in this repo.

The boundary is the `## Personalize` block at the top of each skill file: paths and personal conventions above the line, engine below. Updating the engine means replacing everything below the block; personal settings survive.

## The loop, step by step

### 1. Observe

After each finished piece, the skill reflects on what the user's reactions revealed and proposes one terse, dated bullet for the style guide's `## Observed patterns` log. Always shown before writing; the user approves every learning.

The highest-signal entry format is an exact before/after pair:

> 2026-07-02: "off the table" -> "we weren't able to use". Set-phrase idioms stand out against my plain tone.

Pairs beat described rules because the next draft can be audited against the literal string, and the correction preserves the user's own replacement wording.

If nothing new was revealed, skip. A padded log drowns the real signal.

### 2. Promote

A pattern's **second occurrence** is the promotion trigger. The skill proposes moving the rule to its proper standing home:

| Rule kind | Home |
|---|---|
| How I always write | Core voice |
| A phrasing I reach for | Phrasing bank |
| A phrasing to never use | Scrub list |
| Specific to one person | Their Recipients entry |
| Specific to one kind of email | The Email types map |

Promotion mechanics that keep the system honest:

- **Mark, don't delete.** Promoted bullets stay in the log suffixed `(promoted to X, YYYY-MM-DD)`. The log is the audit trail of how the voice model evolved.
- **Newest wins.** A new observation contradicting an old one supersedes it; the old bullet gets `(superseded YYYY-MM-DD)` rather than deletion.
- **Distill under pressure.** Past ~25 unpromoted entries, run a distillation pass (promote, consolidate, mark) instead of appending blindly. Append-only logs rot.

### 3. Audit

Every promoted rule feeds the mandatory pre-output audit: before the user sees any draft (including every revision), the skill checks it against the scrub list and the AI-tell catalog, and fixes violations silently. This is what converts logged learnings into felt improvement; rules that aren't enforced at generation time are just notes.

The audit carries one standing caveat: **the test is sincerity, not blandness.** A user's genuine warmth, hedging, or effusiveness is voice, and the audit must never strip it. Only phrasing that sounds generic or performative gets cut.

### 4. Route

Not every learning belongs to this profile. When a correction generalizes ("never em dashes, anywhere"), it should live at the most general applicable layer, and the profile keeps only an *echo* that names its canonical source. Echoes at the point of enforcement are deliberate and good; unattributed copies drift.

## Why examples outrank rules

Real approved examples (the style guide's `## Good examples`) outrank every written rule, because rules are lossy compressions of taste. The skill matches examples first, rules second, generic writing advice never. This is also why the fastest way to bootstrap a profile is pasting in 2-3 real pieces the user was happy with.

## Recipient/context profiles

Voice varies by audience. A `## Recipients` section holds one entry per recurring recipient: formality rung, register, standing context, links to prior drafts. Two enforcement details:

- Prior drafts to the same person are checked to **avoid reusing exact phrases** (gratitude lines and closers age fastest).
- A new recipient is not a cold start: the closest entry in the types map plus the global voice layers covers everything except person-specific context, which is exactly and only what the skill asks about.

## What "improving the skill" means

Three distinct things improve, at three speeds:

1. **The data** improves every use (observed patterns, promotions). Private, automatic.
2. **The engine** improves when a process gap is found (a missed audit, a better promotion rule). Those changes belong below the Personalize line and are shareable to everyone via this repo.
3. **The seed templates** improve when a FILL-ME prompt turns out to confuse new users. Also shareable.

When you fix something locally, ask which of the three it is; that answers where the change goes.
