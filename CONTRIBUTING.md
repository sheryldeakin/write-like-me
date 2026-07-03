# Contributing

Contributions welcome. The one rule that decides most calls: **engine and data stay separate.**

- The **engine** (skill instructions, learning protocol, generator, templates) is shared and must work for anyone. Nothing person-specific belongs in it, including disguised person-specific defaults. Example of the bug class: the engine once said "never strip warmth or polite hedging; that's my voice." True for one author, wrong for a blunt one. The fix deferred to the style guide instead. If you find an assumption like that in the engine, that's a bug report we want.
- The **data** (anyone's actual style guide, phrasing bank, recipients, drafts) never enters this repo, including in examples. The walkthrough uses invented people; keep it that way.

## What's welcome

- **AI-tell catalog patterns** (`reference/ai-writing-forbidden-patterns.md`): new patterns with a couple of real-ish examples and, ideally, which existing category they extend. The Standing rules section describes the meta-principles a pattern should fit.
- **Engine improvements**: gaps in the loop (a missed audit condition, a better promotion rule, a cold-start improvement). Engine changes apply to every profile, so they need to be person-agnostic and category-agnostic.
- **Template and docs clarity**: anywhere a FILL-ME prompt or setup step confused you, that confusion is signal. The quick start has been dry-run once; more real setup reports help.
- **Generator improvements** (`generator/skill.md`): better interview questions, better anatomy mapping for genres it handles badly.
- **Curated profiles**: a new `profiles/{category}/` is welcome once it has been genuinely used and calibrated by a real person for a while, with its data scrubbed to empty templates. Untested guess-profiles are what the generator is for.

## House style

- No em dashes anywhere in the repo. The project practices its own catalog; people will grep for exactly this.
- Plain prose. Run your text against `reference/ai-writing-forbidden-patterns.md` before opening a PR; it's the review standard for docs.

## Process

Open an issue or PR on GitHub. Small fixes can go straight to PR; for engine changes, an issue first saves everyone time because engine behavior is deliberately conservative.
