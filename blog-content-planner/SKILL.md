---
name: blog-content-planner
description: Plans and drafts the next blog post for ANY product, SaaS, or website — not tied to one company. Use whenever the user asks to plan or write a blog post for their site, run a recurring content/blog task, find the next blog topic, do content-gap or competitor content research, or wants an AI-image-generator prompt for a blog thumbnail. On first use for a given site it interviews the user once (site, blog URL, competitors, audience, output format) and saves the answers, so later runs — including unattended scheduled/recurring tasks — don't need to ask again.
---

# Blog Content Planner

Produces one complete blog post plan/draft per run for a given site, plus an AI-image-generator prompt for its thumbnail. Works for any product by keeping a per-site profile and topic log under `references/projects/`.

## Step 0: Identify the project and load or create its profile

Slugify the site's domain or product name (e.g. `vetvertex-com`, `acme-app`) and look for `references/projects/<slug>/profile.md`.

**If it exists:** load it and skip straight to Step 1 — this is what lets a recurring/scheduled task run unattended without a human to answer questions.

**If it doesn't exist:** this is a first run for this site. Interview the user once (use multiple-choice tools if available, otherwise ask plainly):
1. Site URL, and product/feature summary (or offer to fetch the homepage and infer it)
2. Does a blog already exist at a URL? If yes, get it. If no, note that there's no live blog to cross-check and rely solely on the topic log.
3. Who publishes — does this skill just draft, or does the user want it auto-formatted for a specific CMS? (Default: draft only, user publishes manually.)
4. Competitors to check for content gaps (names or URLs) — ask explicitly; don't guess competitors.
5. Target audience / tone (e.g. "small business owner, plain language" vs "developer-facing, technical")
6. Output preference: full ready-to-publish draft vs outline only

Save the answers to `references/projects/<slug>/profile.md` (template below) and create an empty `references/projects/<slug>/topics-log.md`. Confirm the setup with the user once, then proceed.

**If the skill folder isn't writable** (some environments mount installed skills read-only), don't fail: show the user the finished profile text and ask them to save it somewhere persistent — e.g. paste it into their scheduled-task prompt or a project file — and on later runs accept the profile from the task prompt or conversation instead. When a live blog URL exists, the blog itself is the topic history, so the log is only a convenience cache.

## Step 1: Sync the topic log

If the profile has a live blog URL, fetch it and reconcile its actual post list against `topics-log.md` — add anything missing, note if the fetch fails and fall back to the log alone. If there's no live blog, the log is the only record; trust it.

## Step 2: Refresh product context

Re-fetch the site's homepage/features page if it's been a while, to catch any product changes since the profile was written. Don't re-interview the user for this — just note observed changes.

## Step 3: Competitor scan — always, using the profile's competitor list

For each competitor, check recent content/blog activity. Look for: topics they cover that this site doesn't, gaps neither side covers, and any positioning worth countering.

## Step 4: Pick the topic

Cross-reference topic log + competitor scan + product features. Pick ONE topic that's unlogged, ties to a real feature or real audience pain point, and ideally exploits a competitor gap. State the pick and one-line reasoning before drafting — unless this is an unattended/scheduled run, in which case proceed directly and just include the reasoning in the delivered output.

## Step 5: Draft

Per the profile's output preference (full draft or outline). A full draft includes: SEO title (~60 chars), meta description (~155 chars), Markdown body with 2-4 subheadings, closing CTA, ~600-900 words unless told otherwise. Match the tone/audience from the profile.

## Step 6: Thumbnail image prompt

Write one ready-to-paste prompt for an AI image generator (Midjourney/DALL-E/Stable Diffusion/Ideogram, etc.), tailored to the post's topic and the profile's brand feel. Include:
- Subject and composition (what's literally depicted)
- Visual style (e.g. clean flat illustration, modern photo-real, isometric — infer from the site's existing look if known, otherwise default to clean modern flat illustration)
- Color direction (use brand colors if known)
- Aspect ratio: 16:9 (standard blog thumbnail) unless the user wants square/other
- Explicitly instruct the model to avoid rendering embedded text/words in the image (AI image generators render text unreliably) — the post title will be overlaid separately if needed

## Step 7: Log and deliver

Append the new topic (date, topic, angle) to `topics-log.md`. Deliver the draft as a file, plus the thumbnail prompt as plain text the user can copy straight into any image generator.

## Profile template (`references/projects/<slug>/profile.md`)

```markdown
# <Site Name> — Blog Planner Profile

- Site URL:
- Blog URL: (or "none — log-only")
- Product/features summary:
- Competitors:
- Audience/tone:
- Output preference: full draft | outline only
- Publishing: manual | (CMS/format notes)
```

## Topic log template (`references/projects/<slug>/topics-log.md`)

```markdown
# <Site Name> Blog Topic Log

| Date | Topic | Angle |
|------|-------|-------|
```

## Notes

- Never invent competitors or a blog URL the user didn't confirm — ask once, then trust the saved profile.
- One profile + log per site, so this skill safely handles multiple products without mixing up topic history.
- If the user's product or competitors change materially, update the profile file rather than re-interviewing from scratch — just edit the relevant field.
