# /email: Draft an email with Claude, in my voice

Reduce the blank-page block on email. Load my standing email style guide, take the task, draft in my voice, and iterate until it's right. Also quietly learn how I write so the skill improves over time.

## Personalize

<!-- EDIT THIS BLOCK ONLY. Everything below it is the engine (from
     github.com/sheryldeakin/write-like-me). To update the engine later,
     replace everything below this block with the newer version; your
     settings here survive. -->

- **Style guide:** `~/writing-voice/email.md`
- **Snippets:** `~/writing-voice/snippets.md`
- **Drafts folder:** `~/writing-voice/drafts/`
- **AI-tell catalog:** `~/writing-voice/ai-writing-forbidden-patterns.md` (optional; from the repo's `reference/`)
- **Note conventions:** none. <!-- If your notes system has rules (frontmatter, tags, linking), state them here and they apply to saved drafts. -->

## Usage

- `/email <task>`: one-line task, e.g. `/email reschedule Thursday's advisor meeting to next week`
- `/email`: no task; ask me what the email needs to do

## Instructions for Claude

### Step 1: Load my voice

Read the style guide in full: Core voice, the four-part skeleton, the tone ladder, conciseness rules, anti-patterns, the `## Email-specific tells` scrub list, the `## Phrasing bank` (my calibrated go-to phrasings), the `## Email types and tone` map, the `## Recipients` profiles, `## Observed patterns`, and any `## Good examples`. Read the snippets file for more reusable phrasings. The `## Good examples` (real emails I liked) outrank any written rule; match those first. Reach for the `## Phrasing bank` phrasings as defaults. In the `## Email types and tone` map, find the entry closest to the email I'm writing and start the tone from there (open its linked draft as a worked example if useful). Honor the AI-tell catalog with the sincerity caveat: my sincere warmth and hedging are voice, not tells.

### Step 2: Understand the task

Parse the task from the argument. Before asking me anything, check `## Recipients` in the style guide:

- **Known recipient (has an entry):** take the rung, register, and standing context from the entry, and skim their linked prior drafts to match the established register and avoid reusing exact phrases with them (especially gratitude lines and closers).
- **New recipient (no entry):** don't start cold. Pick the closest entry in `## Email types and tone` and start from that tone; the Core voice, Phrasing bank, scrub list, and Good examples encode everything past emails have taught, and they apply to every recipient. Only the person-specific context (rung, history, quirks) is missing, so that's what to ask about.

Then ask ONLY for what you genuinely can't infer; keep it to one tight round, not an interrogation. Usually you need:

- **Recipient + relationship:** who, and do we have prior history? (sets the tone-ladder rung and whether to use a warm opener)
- **The core ask / goal:** what the email must accomplish
- **Hard constraints:** dates, facts, names, links, anything that must appear or must not

If the task line already answers these, skip the questions and draft.

### Step 3: Draft

Write the email using the four-part skeleton at the right rung. Warm opener when there's prior connection; polite request framing for any ask; clear next step left open enough for them to adjust. Keep it concise but never cold.

**Before showing any draft (including every revision in Step 4), run a final audit on the text:** no formatting tells, no emojis, no set-phrase idioms or corporate phrasing (check the `## Email-specific tells` scrub list in the style guide), and no AI-tell-catalog patterns that fail the sincerity test. Fix silently before outputting. The audit is mandatory, not optional.

Output the draft as plain email text (Subject line + body), ready to paste, not wrapped in commentary. Briefly note the rung you chose and any assumption you made, below the draft.

### Step 4: Iterate

I react in plain language ("too formal", "cut paragraph two", "add that I'll send the file separately"). Revise and re-output the full email. Repeat until I say it's done. I don't need to articulate what's wrong in writing terms; translate my reaction into the edit.

### Step 5: Offer to save

When I'm happy, offer to save the final to the drafts folder as `YYYY-MM-DD-{slug}.md`. Body: the final email under an H1 title, plus a one-line context note, plus links to related notes if my note conventions call for them. Only save if I say yes (some emails aren't worth keeping). If the email is one I clearly liked, also offer to add it under `## Good examples` in the style guide: a link to the draft plus one line on why it worked, not a second full copy of the email.

**Chains:** if the email continues an ongoing chain that already has a saved draft (check the recipient's `## Recipients` entry), offer to append it to that draft under a `## Thread continued` heading (dated, including any replies worth keeping) instead of creating a new file. One file per chain.

### Step 6: Learn (the part that improves the skill)

After the email is settled, reflect on what this round revealed about how I write, and append a terse dated bullet to the `## Observed patterns` section of the style guide. Capture things like:

- Phrasings / openers / sign-offs I reached for or kept
- Edits I made consistently (e.g. "softened every direct ask", "cut the backstory paragraph")
- Tone calibration I corrected (drafted rung vs. what I actually wanted)

Show me the addition before writing it. Keep entries short. If nothing new was revealed, say so and skip; don't pad the log.

**Entry format:** prefer exact before/after phrase pairs ("off the table" -> "we weren't able to use") over described rules; they're the highest-signal format. Date every entry.

**Promotion mechanics (check on every append):**
- Before appending, scan the log for a similar existing entry. A second occurrence is the promotion trigger: propose promoting the rule to its proper home (Core voice, Phrasing bank, scrub list, or a Recipients entry). Don't do it silently.
- When a rule is promoted, don't delete the log bullets; suffix them with "(promoted to X, YYYY-MM-DD)". The log is the audit trail.
- If a new observation contradicts an older one, newest wins: append the new entry and suffix the old one with "(superseded YYYY-MM-DD)".
- If unpromoted entries exceed ~25, propose a distillation pass (promote, consolidate, mark) instead of appending blindly.

Also update the `## Email types and tone` map: if this email fits an existing type, extend that entry with anything new I learned; if it is a new type, add a short entry (the type, the recipient relationship, the tone that worked, and a link to the saved draft). This is how the map grows over time. Same show-first rule.

Also update `## Recipients`: if the round revealed something durable about a recurring recipient (register, preferences, standing context, a new chain), offer to update their entry, or create one if this looks like someone I'll email again. Same show-first rule.

**Learn from replies too:** when a chain file contains the recipient's replies, mine them for durable facts about the person (their register and sign-off, stated constraints and availability like "away until August" or "email is easier than meeting", what they respond well to) and propose those into their `## Recipients` entry alongside what my own corrections revealed.

## Rules

- Match `## Good examples` over abstract rules; match my Observed patterns over generic advice.
- Never strip warmth or polite hedging in the name of conciseness; that's my voice, not a flaw.
- One tight round of clarifying questions, not many.
- Output drafts as paste-ready email text, not buried in prose.
- Show the change before writing to the style guide or saving a draft; never silently edit my notes.
- No emojis in the email or the notes.
