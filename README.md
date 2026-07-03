# write-like-me

A self-improving writing-voice system for [Claude Code](https://claude.com/claude-code). It drafts in your voice, learns from every correction you make, and gets better the more you use it.

## Why this exists

I have rewritten a two-line email eleven times and then closed the tab. Email has always been a dead stop for me: a five-minute task that parks itself in front of everything else on my list and idles there for days while I avoid it like the plague. I know how ridiculous that is. Knowing has never fixed it.

So I built the thing I needed. I tell Claude what the email has to do, it drafts in my voice, I react in plain language ("too formal", "cut paragraph two"), and we keep going until it's right. No blank page, ever. The system also pays attention while we work: it logs what my corrections reveal about how I write, and the patterns that keep showing up become standing rules that every future draft is checked against. The first drafts keep getting closer to something I would have written on a good day.

I didn't build this to outsource my writing. I built it because a five-minute email should cost five minutes, and the hours I used to lose circling one belong to work that needs them. I can't be the only one who does this. Email is the first profile. Papers and other writing are on the roadmap, because the blank page is the same problem everywhere.

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

Full protocol: [docs/learning-loop.md](docs/learning-loop.md). To see the loop play out over three weeks with a fictional user, read the [example walkthrough](docs/example-walkthrough.md).

## Quick start

1. Create a folder for your voice data (anywhere: a notes vault, `~/writing-voice/`, a private repo). Copy `email.md` and `snippets.md` from `profiles/email/templates/` into it, create a `drafts/` subfolder, and copy `drafts-index.md` into it as `drafts/index.md`.
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
generator/
  skill.md            /new-profile: generate a voice profile for any writing category
templates/
  shared-core.md      cross-profile rules every profile reads (learned once, inherited everywhere)
docs/
  learning-loop.md    the full learning protocol (observe -> log -> promote -> audit)
  example-walkthrough.md   three weeks of the loop with a fictional user
reference/
  ai-writing-forbidden-patterns.md   catalog of AI-tell patterns, organized A-T
```

## Beyond email: any category of writing

Email is the hand-built reference profile, and it plays two roles: the fastest on-ramp (copy its templates and run `/email` if email is your pain point) and a worked example of the standard profile anatomy that every generated profile follows, so reading `profiles/email/` shows you what a mature profile looks like before you generate your own. The engine underneath it is category-agnostic. `generator/skill.md` installs as `/new-profile`: name a kind of writing you do repeatedly (weekly lesson scripts, client proposals, grant applications), and it interviews you, optionally researches the genre's conventions, and generates a complete profile: a style guide in the standard anatomy plus a drafting skill running the exact same learning loop. Your pasted examples outrank the researched conventions wherever they conflict, and the profile calibrates itself from there the same way email does.

## The AI-tell catalog

`reference/ai-writing-forbidden-patterns.md` is a curated catalog of patterns that read as AI-generated in formal writing: punctuation tells, discourse markers, cleft sentences, hyperbolic intensifiers, meta-claims, hedge stacking, and more, plus meta-principles for catching new instances. It was built up across many cleanup passes on real academic prose. The email skill uses it in the pre-output audit with one caveat baked in: sincere warmth and hedging are voice, not tells. The test is sincerity, not blandness.

## Roadmap

- `profiles/paper/`: a curated academic-writing profile (section drafting, figure commentary, structural moves), once it has been calibrated on a real paper the way email was calibrated on real emails.
- Sent-folder bootstrap: point the skill at an export of your sent mail (a Gmail Takeout mbox, a folder of .eml files) and mine your actual voice at scale, locally: phrasing bank, recipient profiles, and types map seeded from hundreds of real emails in one pass instead of one cold-start question.
- Cross-profile promotion: a rule learned in email that generalizes ("never em dashes") routing up to a shared core all profiles read.

The `profiles/` layout and the generator exist so all of this slots in without restructuring.

## License

MIT.
