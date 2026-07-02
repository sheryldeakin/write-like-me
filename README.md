# write-like-me

A self-improving writing-voice system for [Claude Code](https://claude.com/claude-code). It drafts in *your* voice, learns from every correction you make, and gets better the more you use it.

You type `/email follow up with my advisor about the meeting`, react in plain language ("too formal", "cut paragraph two"), and the system revises until it's right. Behind the scenes it logs what your corrections reveal about how you write, promotes repeated observations into standing rules, and audits every future draft against them. After a few weeks, first drafts start coming out sounding like you.

## How it works: engine vs. data

The system splits into two layers:

- **The engine** (this repo): skill instructions and the learning protocol. How to draft, how to iterate, how to log observations, when to promote them into rules, what to audit before showing you anything. Nothing about any specific person.
- **The data** (your private notes, never in this repo): your style guide, your phrasing bank, your recipient profiles, your saved drafts, your observed-patterns log. These files start as the empty templates in `profiles/email/templates/` and fill themselves through use.

You clone the engine; your data grows locally. Improvements to the engine can be shared without your data ever leaving your machine.

## The learning loop

1. **Draft** — the skill reads your style guide (voice rules, phrasing bank, recipient profiles) and drafts. Before showing you anything, it audits the text against your scrub list and the [AI-tell catalog](reference/ai-writing-forbidden-patterns.md).
2. **Iterate** — you react in plain language. You never need to name the problem in writing terms; the skill translates your reaction into the edit.
3. **Observe** — after the email settles, the skill proposes a one-line dated entry to your observed-patterns log. The highest-value format is an exact before/after pair: `"off the table" -> "we weren't able to use"`.
4. **Promote** — the second time a pattern shows up, the skill proposes promoting it to a standing rule (core voice, phrasing bank, scrub list, or a recipient profile). Promoted log entries are marked, not deleted; contradictions resolve newest-wins. The log is the audit trail.
5. **Audit** — promoted rules feed the mandatory pre-output audit, so every future draft is checked against everything the system has learned.

Full protocol: [docs/learning-loop.md](docs/learning-loop.md).

## Quick start

1. Create a folder for your voice data (anywhere — a notes vault, `~/writing-voice/`, a private repo) and copy the three files from `profiles/email/templates/` into it.
2. Copy `profiles/email/skill.md` to `~/.claude/commands/email.md` (macOS/Linux) or `%USERPROFILE%\.claude\commands\email.md` (Windows).
3. Edit the `## Personalize` block at the top of that file: point the three paths at your voice-data folder. Everything below the block is the engine — leave it alone (updating it later = pasting in the new version from this repo).
4. Optionally copy `reference/ai-writing-forbidden-patterns.md` next to your voice data so the audit step can use the full catalog.
5. In Claude Code, run `/email <what the email needs to do>` and start reacting.

The style guide bootstraps fastest if you paste 2-3 real emails you were happy with under its `## Good examples` section — real examples outrank any written rule.

## What's in the box

```
profiles/
  email/
    skill.md          the /email skill (copy to ~/.claude/commands/, edit Personalize block)
    templates/
      email.md        style-guide skeleton: voice rules + empty banks that fill through use
      snippets.md     neutral seed phrasings to calibrate over time
      drafts-index.md index for your saved drafts folder
docs/
  learning-loop.md    the full learning protocol (observe -> log -> promote -> audit)
reference/
  ai-writing-forbidden-patterns.md   catalog of AI-tell patterns, organized A-T
```

## The AI-tell catalog

`reference/ai-writing-forbidden-patterns.md` is a curated catalog of patterns that read as AI-generated in formal writing: punctuation tells, discourse markers, cleft sentences, hyperbolic intensifiers, meta-claims, hedge stacking, and more, with meta-principles for catching new instances. It was built up across many cleanup passes on real academic prose. The email skill uses it in the pre-output audit with one important caveat baked in: *sincere* warmth and hedging are voice, not tells. The test is sincerity, not blandness.

## Roadmap

The email profile is the first of several planned voice profiles built on the same protocol:

- `profiles/paper/` — academic-writing voice: section drafting, figure commentary, structural moves.
- Cross-profile promotion: a rule learned in email that generalizes ("never em dashes") routing up to a shared core.

The `profiles/` layout exists so these slot in without restructuring.

## License

MIT.
