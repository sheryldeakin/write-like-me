# /new-profile: Generate a writing-voice profile for any category

Create a complete voice profile (style guide + drafting skill) for a new kind of writing: weekly lesson scripts, client proposals, grant applications, sermon notes, changelogs, whatever the user writes repeatedly. The engine mechanics are identical across every profile; only the genre-specific parts get generated.

Install: copy this file to `~/.claude/commands/new-profile.md` and edit the Personalize block.

## Personalize

<!-- EDIT THIS BLOCK ONLY. -->

- **Voice-data root:** `~/writing-voice/` (each profile gets a subfolder)
- **Commands folder:** `~/.claude/commands/` (where generated skills go)
- **Web research:** allowed <!-- set to "not allowed" to skip the conventions-research step -->
- **AI-tell catalog:** `~/writing-voice/ai-writing-forbidden-patterns.md` (shared across profiles)

## Usage

- `/new-profile <category>`, e.g. `/new-profile weekly lesson scripts`
- `/new-profile` with no argument: ask what kind of writing this is for

## Instructions for Claude

### Step 1: Interview (one tight round)

Ask only what the generator genuinely needs, in a single round:

- **The category, in the user's words.** Also ask what one finished piece is called (a script, a proposal, a lesson plan); that noun labels everything.
- **Audience and stakes.** Who reads or hears it, what happens if it's good or bad, and whether the audience recurs (recurring audiences get context profiles, like recipients in the email profile).
- **Cadence.** Weekly? Per client? Per semester? This decides whether chains and types matter.
- **1-3 real examples, pasted.** Strongly encourage this; real examples outrank everything the generator will write. If the user has none, note that the first-use cold start will handle it.
- **What good looks like, and known pet peeves.** In their words.

If the category is really an existing profile in disguise (a "client update email" is the email profile), say so and stop instead of generating a duplicate.

### Step 2: Research the genre's conventions (if web research is allowed)

Search for the genre's established conventions and structures: how practitioners structure the piece, what the known failure modes are, what the respected guides say. Distill into two short lists:

- **A structural skeleton:** the 3-6 slots a finished piece needs, in order. This replaces the email profile's four-part skeleton. Derive it from the research AND the user's pasted examples; when they conflict, the user's examples win.
- **Starter conventions:** 5-10 genre-specific dos and don'ts, each marked as a default to calibrate away from, with sources noted.

Present both for reaction before using them. If research is not allowed or turns up little, derive the skeleton from the pasted examples alone and say so.

### Step 3: Generate the style guide

Create `{voice-data root}/{category-slug}/{category-slug}.md` following the standard profile anatomy. Every profile has the same sections so the learning loop works identically everywhere:

1. **Core voice**: seeded from the pasted examples if any, otherwise FILL-ME prompts adapted to the genre.
2. **Structural skeleton**: from Step 2, named for the genre.
3. **Tone/register map**: the audience analog of the email tone ladder (rungs for a class vs. a parent email vs. an admin report, for example). Genre-appropriate rung names.
4. **Conciseness and format rules**: genre defaults (target length, sections, slides vs. prose) marked as calibratable.
5. **Scrub list**: seeded with em dashes plus genre cliches from the research.
6. **Phrasing bank**: mined from the pasted examples, empty categories otherwise.
7. **Types map**: kinds of pieces within the category, grows through use.
8. **Context profiles**: the recipients-analog, named for the genre (Audiences, Classes, Clients, Venues). Same entry shape: register, standing context, prior pieces, mine-their-responses rule where responses exist.
9. **Observed patterns**: the standard lifecycle text, verbatim from the email template (second occurrence promotes, promoted entries marked, newest wins, distill past ~25).
10. **Good examples**: the pasted examples, each with one line on why it represents the user's voice.

### Step 4: Generate the skill

Create `{commands folder}/{category-slug}.md`: the email engine with genre nouns swapped and nothing else changed. Same six steps (load voice, understand the task, draft with cold start and mandatory audit, iterate on plain-language reactions, offer to save with chains, learn with promotion mechanics), same rules section, same show-first discipline. Fill its Personalize block with the new profile's paths. The engine mechanics are not adjustable per category; if a category seems to need different mechanics, that's an engine improvement and belongs upstream in the repo.

### Step 5: Hand off

Show the user everything before writing any file (style guide, skill, both paths). After they approve, confirm what to type for their first run (`/{category-slug} <task>`) and remind them the first use will run cold-start calibration if the guide is thin.

## Rules

- Show everything before writing it; never generate files silently.
- The user's pasted examples outrank researched conventions everywhere they conflict.
- Researched conventions are seeds marked for calibration, not rules; the user's corrections will overwrite them and that is the point.
- One profile per genuinely distinct kind of writing. When in doubt, extend an existing profile's types map instead.
- No em dashes in any generated file.
