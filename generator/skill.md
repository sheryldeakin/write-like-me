# /new-profile: Generate a writing-voice profile for any category

Create a complete voice profile (style guide + drafting skill) for a new kind of writing: weekly lesson scripts, client proposals, grant applications, sermon notes, changelogs, whatever the user writes repeatedly. The engine's *mechanics* (draft, iterate, observe, promote, audit) are identical across every profile; the genre-specific *content* gets generated. This skill's job is to adapt the engine to a genre without leaving email's fingerprints on it.

Install: copy this file to `~/.claude/commands/new-profile.md` and edit the Personalize block.

## Personalize

<!-- EDIT THIS BLOCK ONLY. -->

- **Voice-data root:** `~/writing-voice/` (each profile gets a subfolder)
- **Commands folder:** `~/.claude/commands/` (where generated skills go)
- **Web research:** allowed <!-- set to "not allowed" to skip the conventions-research step -->
- **Shared AI-tell catalog:** `~/writing-voice/ai-writing-forbidden-patterns.md` (one copy, shared across all profiles)

## Usage

- `/new-profile <category>`, e.g. `/new-profile weekly lesson scripts`
- `/new-profile` with no argument: ask what kind of writing this is for

## Instructions for Claude

### Step 1: Interview (one tight round)

Ask only what the generator genuinely needs, in a single round:

- **The category, in the user's words.** Also ask what one finished piece is called (a script, a proposal, a lesson plan). That noun labels everything downstream.
- **Audience and stakes.** Who reads or hears it, what happens if it's good or bad, and **whether the audience is one recurring group, many distinct recipients, or a broad/anonymous public.** This single answer decides the shape of the context-profiles section (see Step 3, section 8), so get it explicitly.
- **Is there a written reply channel?** Do readers write back in a way worth learning from (email replies, PR comments), or is it one-directional (a lesson delivered aloud, a published post)? This decides whether the reply-mining mechanic is included at all.
- **Cadence.** Weekly? Per client? Per semester? Decides whether chains and a types map matter.
- **1-3 real examples, pasted.** Strongly encourage this; real examples outrank everything the generator will write. If the user has none, say the first-use cold start will handle it, and note that the tone map and conventions will be provisional until real pieces exist. If an example arrives obviously truncated or unusable (a title fragment, a cut-off paste), do not mine it: say so, offer to let them re-paste, and otherwise treat it as no-example rather than seeding from garbage.
- **What good looks like, and known pet peeves,** in their words. Capture the pet peeves literally; they seed the anti-patterns section, which is mandatory (see section 6 below). A stated pet peeve must never fall through.

If the category is really an existing profile in disguise (a "client update email" is the email profile), say so and stop instead of generating a duplicate.

### Step 1b: Derive the slug and command name

From the piece-noun (not the raw category phrase), derive one **kebab-case slug**, singular, no filler words: "weekly lesson scripts" with piece-noun "lesson script" becomes `lesson-script`. This slug names the profile folder, the style-guide file, the skill file, and the `/command`. **Before committing to it, check the commands folder for an existing `{slug}.md`;** if one exists, propose an alternative (a prefix or a fuller form) rather than clobbering it. Show the user the chosen slug and the resulting command they will type, and let them override it. Everything downstream uses this one slug.

### Step 2: Research the genre's conventions (if web research is allowed)

Search for the genre's established conventions and structures: how practitioners structure the piece, what the known failure modes are, what the respected guides say. Distill into two short lists:

- **A structural skeleton:** the 3-6 slots a finished piece needs, in order. This replaces the email profile's four-part skeleton. Derive it from the research AND the user's pasted examples; when they conflict, the user's examples win.
- **Starter conventions:** 5-10 genre-specific dos and don'ts, each marked as a default to calibrate away from, with sources noted. **Mark any convention you are not confident about as low-confidence explicitly** (thin sourcing, niche genre, conflicting practice), so the user knows which seeds to distrust.

Present both for reaction before using them. If research is not allowed or turns up little, derive the skeleton from the pasted examples alone and say so; if there are also no examples, say the skeleton is provisional and lean on cold-start calibration at first use.

### Step 2b: Ensure the voice-data root exists

Before generating, check that the voice-data root exists and that the shared AI-tell catalog is present at the path in the Personalize block. If the root is missing, create it. If the catalog is missing, copy it from the write-like-me repo's `reference/ai-writing-forbidden-patterns.md`, or, if the repo isn't available on this machine, tell the user where to get it and set the generated skill's catalog line to "(none yet)" so it doesn't reference a file that isn't there. A generated skill must never point its Personalize block at a file that doesn't exist.

### Step 3: Generate the style guide

Create `{voice-data root}/{slug}/{slug}.md`. Use the section list below. Sections marked **[loop]** are mandatory and must appear in every profile unchanged in *purpose* (they are what makes the learning loop work). Sections marked **[adapt]** are shaped to the genre. Sections marked **[drop-if-NA]** are omitted when the genre doesn't need them, with a one-line note saying why.

Critical rule: **generate, don't transplant.** Do not copy email-template prose verbatim. Any sentence you carry over must be rewritten in the genre's nouns. After writing the file, re-read it and confirm no residual "email", "recipient", "Subject line", "sign-off", or similar email-only word survives except where it genuinely applies.

1. **Intro + how to use** [adapt]: one short paragraph, genre-named.
2. **Core voice** [loop]: seeded from pasted examples if any, otherwise FILL-ME prompts written for *this* genre (not email's prompts).
3. **Structural skeleton** [adapt]: from Step 2, named for the genre (a "Lesson arc", a "Proposal shape").
4. **Tone / register map** [drop-if-NA]: include only rungs the user actually writes for. If the user writes for a single context, replace the table with one line naming that register, and say the map will grow if new contexts appear. Never invent rungs the user did not indicate.
5. **Conciseness and format rules** [adapt]: genre defaults (length, sections, prose vs. slides vs. script beats), each marked calibratable.
6. **Anti-patterns + scrub list** [loop]: two parts. First, the user's stated pet peeves as an explicit "things I want to stop doing" list (this is where the interview's pet peeves land; it is mandatory and must not be dropped). Second, the machine-auditable scrub list, seeded with em dashes plus any genre cliches from the research.
7. **Phrasing bank** [adapt]: category headers invented for the genre (a lesson script has Hooks / Explanations / Build prompts, not Openers / Sign-offs). Mined from pasted examples; empty headers otherwise.
8. **Context profiles** [adapt to the Step 1 audience answer]:
   - *Many distinct recipients* (like email): a "Recipients"-style section, one entry per person, with the pick-the-closest and avoid-reused-phrasing machinery.
   - *One recurring audience* (like a class): a single "Audience" entry describing that group. Do NOT generate the multi-entry pick-one machinery; there is nothing to pick between. The skill's Step 2 branch is simplified accordingly (see Step 4).
   - *Broad / anonymous public* (like a blog): drop per-entity profiles entirely; replace with a short "Who this is for" note about the general reader.
9. **Observed patterns** [loop]: the standard lifecycle, rewritten in genre nouns. Keep the mechanics exactly (second occurrence promotes; promoted entries suffixed and kept; newest wins; distill past ~25) but do not carry the email wording. Reference the section names that actually exist in *this* guide.
10. **Good examples** [loop]: the pasted examples, each with one line on why it represents the user's voice; a "none yet, cold start will seed this" note otherwise.

### Step 4: Generate the skill

Create `{commands folder}/{slug}.md`: the email engine adapted to this genre. Same six steps and same mechanics (load voice; understand task with cold-start; draft with the mandatory pre-output audit; iterate on plain-language reactions; offer to save with chains; learn with promotion mechanics), but adapt these genre-specific points rather than copying them:

- **Output format** in Step 3: the email engine says "plain email text (Subject line + body)". Replace this with the genre's real output shape (a lesson script has beat headers, not a subject line). Do not leave "Subject line" in a non-email skill.
- **Context-profile branch** in Step 2: match section 8 above. For a single recurring audience or a public genre, remove the "known recipient vs. new recipient, pick the closest entry" branching; there is nothing to disambiguate. Keep only "load the audience context and avoid repeating recent pieces."
- **Reply-mining** in Step 6: include the "learn from replies" instruction ONLY if Step 1 established a written reply channel. For one-directional genres, drop it entirely rather than leaving a mechanic that can never fire.
- **Chains** in Step 5: keep only if the genre has a real thread analog (an email chain, a revised proposal). For serial-but-independent pieces (a new lesson each week), say one file per piece and drop the "Thread continued" append.
- **Nouns** everywhere: email/message/recipient/sign-off become the genre's words.
- **Snippets file:** the email profile ships a separate `snippets.md`; generated profiles do not (the style guide's Phrasing bank serves the same role). Omit the snippets path from the generated Personalize block and drop the "read the snippets file" clause from the skill's Step 1, so nothing references a file that doesn't exist.

Fill the skill's Personalize block with the new profile's paths. Stamp it, just below the Personalize block, with a generation-metadata line:

`<!-- generated by /new-profile from write-like-me engine vX.Y on {date}; audience-shape: <one-recurring|many-recipients|public>; reply-channel: <yes|no> -->`

(Read the engine version from the CHANGELOG or the email skill's version stamp.) This line is what lets a future `/new-profile --regenerate` rebuild the skill against a newer engine while preserving the user's Personalize block and their accumulated style-guide data. The engine mechanics themselves are not adjustable per category; if a genre seems to need different *mechanics* (not content), that is an engine improvement and belongs upstream in the repo, not in one generated skill.

### Step 5: Hand off

Show the user everything before writing any file: the slug and command, the research artifacts, the full style guide, the full skill, and both target paths. After they approve, write the files, confirm the command for their first run (`/{slug} <task>`), and remind them the first use runs cold-start calibration if the guide is thin.

## Rules

- Show everything before writing it; never generate files silently.
- The user's pasted examples outrank researched conventions everywhere they conflict.
- Researched conventions are seeds marked for calibration, not rules; low-confidence ones are flagged as such.
- Generate, don't transplant: no email-template wording survives into a non-email profile. Re-read the generated files and scrub residual email nouns before showing them.
- One profile per genuinely distinct kind of writing. When in doubt, extend an existing profile's types map instead.
- No em dashes in any generated file.
