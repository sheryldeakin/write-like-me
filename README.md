# write-like-me

A self-improving writing-voice system for [Claude Code](https://claude.com/claude-code). It drafts in your voice, learns from every correction you make, and gets better the more you use it.

## Why this exists

I can run experiments, debug a training pipeline, and write a research paper. I have also rewritten a two-line email eleven times and then closed the tab. Email has always been a dead stop for me: a five-minute task that parks itself in front of everything else on my list and idles there for days while I avoid it like the plague. This works about as well as you'd expect for the format the entire professional world runs on.

So I built the thing I needed. I tell Claude what the email has to do, it drafts in my voice, I react in plain language ("too formal", "cut paragraph two"), and we iterate until it's right. No blank page, ever. The system also pays attention: it logs what my corrections reveal about how I write, and the patterns that keep showing up become standing rules that every future draft is checked against. The first drafts keep getting closer to something I would have written on a good day.

The point was never to outsource my writing. The point is that a five-minute email should cost five minutes, and the hours I used to spend circling one are now free for work that deserves them. Email is the first profile. Papers and other writing are on the roadmap, because the blank page is the same enemy everywhere.

## How it works: engine vs. data

The system splits into two layers:

- **The engine** (this repo): skill instructions and the learning protocol. How to draft, how to iterate, how to log observations, when to promote them into rules, what to audit before showing you anything. Nothing in it is about any specific person.
- **The data** (your private notes, never in this repo): your style guide, your phrasing bank, your recipient profiles, your saved drafts, your observed-patterns log. These files start as the empty templates in `profiles/email/templates/` and fill themselves through use.

You clone the engine; your data grows locally. Improvements to the engine can be shared without your data ever leaving your machine.

## The learning loop

1. **Draft.** The skill reads your style guide (voice rules, phrasing bank, recipient profiles) and drafts. Before showing you anything, it audits the text against your scrub list and the [AI-tell catalog](reference/ai-writing-forbidden-patterns.md).
2. **Iterate.** You react in plain language. You never need to name the problem in writing terms; the skill translates your reaction into the edit.
3. **Observe.** After the email settles, the skill proposes a one-line dated entry for your observed-patterns log. The highest-value format is an exact before/after pair: `"off the table" -> "we weren't able to use"`.
4. **Promote.** The second time a pattern shows up, the skill proposes promoting it to a standing rule (core voice, phrasing bank, scrub list, or a recipient profile). Promoted log entries are marked, not deleted; contradictions resolve newest-wins. The log is the audit trail.
5. **Audit.** Promoted rules feed the mandatory pre-output audit, so every future draft is checked against everything the system has learned about you.

Full protocol: [docs/learning-loop.md](docs/learning-loop.md).

## Quick start

1. Create a folder for your voice data (anywhere: a notes vault, `~/writing-voice/`, a private repo) and copy the three files from `profiles/email/templates/` into it.
2. Copy `profiles/email/skill.md` to `~/.claude/commands/email.md` (macOS/Linux) or `%USERPROFILE%\.claude\commands\email.md` (Windows).
3. Edit the `## Personalize` block at the top of that file: point the paths at your voice-data folder. Everything below the block is the engine. Leave it alone; updating it later means pasting in the new version from this repo.
4. Optionally copy `reference/ai-writing-forbidden-patterns.md` next to your voice data so the audit step can use the full catalog.
5. In Claude Code, run `/email <what the email needs to do>` and start reacting.

The style guide bootstraps fastest if you paste 2-3 real emails you were happy with under its `## Good examples` section. Real examples outrank any written rule.

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

`reference/ai-writing-forbidden-patterns.md` is a curated catalog of patterns that read as AI-generated in formal writing: punctuation tells, discourse markers, cleft sentences, hyperbolic intensifiers, meta-claims, hedge stacking, and more, plus meta-principles for catching new instances. It was built up across many cleanup passes on real academic prose. The email skill uses it in the pre-output audit with one caveat baked in: sincere warmth and hedging are voice, not tells. The test is sincerity, not blandness.

## Roadmap

The email profile is the first of several planned voice profiles built on the same protocol:

- `profiles/paper/`: academic-writing voice. Section drafting, figure commentary, structural moves.
- Cross-profile promotion: a rule learned in email that generalizes ("never em dashes") routing up to a shared core.

The `profiles/` layout exists so these slot in without restructuring.

## License

MIT.
