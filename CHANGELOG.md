# Changelog

Engine versions are stamped in each skill file just below the Personalize fence. When the engine version here is newer than yours, replace everything below your fence with the repo version; your Personalize block survives.

## 1.5 (2026-07-02)

- Generator hardened after a clean-room test (simulated `/new-profile weekly lesson scripts` with a fresh agent). Fixes: explicit slug derivation + command-collision check; a "generate, don't transplant" rule so no email wording (recipient, Subject line, sign-off, reply-mining) survives into non-email profiles; anatomy sections tagged [loop] / [adapt] / [drop-if-NA] so single-audience and public genres drop what doesn't fit; a mandatory anti-patterns slot so a stated pet peeve can't fall through; low-confidence research conventions flagged; generation-metadata stamp on generated skills to enable `--regenerate` against a newer engine.

## 1.4 (2026-07-02)

- New: `/new-profile` generator (`generator/skill.md`). Creates a complete voice profile (style guide + skill) for any writing category from an interview, optional genre research, and the standard profile anatomy.
- New: worked example (`docs/example-walkthrough.md`) showing three weeks of the loop with a fictional user.
- New: `CONTRIBUTING.md` and engine version stamps.
- Quick start fix: step 1 now says to create the `drafts/` folder and rename `drafts-index.md` to `drafts/index.md` (found by dry-running the setup).

## 1.3 (2026-07-02)

- Engine: cold-start calibration. On an unseeded style guide, ask for one real sent email to mine, or offer two contrasting drafts and learn from the pick.

## 1.2 (2026-07-02)

- Engine: voice-agnostic. Removed hardcoded warmth/politeness assumptions; the engine now defers to whatever the style guide marks as the user's voice (warmth, hedging, bluntness, formality alike).
- Repo-wide punctuation pass so the project practices its own AI-tell catalog.

## 1.1 (2026-07-02)

- Engine: learn from replies. Chain files containing the recipient's replies get mined for durable recipient facts (register, sign-off, stated constraints).

## 1.0 (2026-07-02)

- Initial release: email profile (skill + templates), learning-loop protocol, AI-tell catalog.
