# Blog Content Planner — a Claude Skill

A [Claude](https://claude.ai) skill that plans and drafts the next blog post for **any** website, SaaS, or product. Point it at your site and it will:

1. Check your live blog so it never repeats a topic
2. Scan your competitors for content gaps
3. Pick the next best topic tied to a real product feature or audience pain point
4. Write a full, ready-to-publish draft (SEO title, meta description, body, CTA)
5. Write a ready-to-paste **thumbnail prompt** for any AI image generator (Midjourney, DALL-E, Stable Diffusion, Ideogram...)

On first use for a site it interviews you once (site, blog URL, competitors, audience, output format) and saves a profile, so later runs, including **unattended scheduled tasks**, don't need to ask again.

## Install

**Claude Code**
```bash
git clone https://github.com/<your-username>/blog-content-planner.git
cp -r blog-content-planner/blog-content-planner ~/.claude/skills/
```
Use `.claude/skills/` inside a repo instead if you want it for one project only.

**claude.ai / Claude desktop**
1. Zip the inner `blog-content-planner/` folder (or download `blog-content-planner.skill` from Releases).
2. Upload it in your Skills settings.

## Usage

Just ask:

> Plan and draft the next blog post for https://yoursite.com

First run: Claude asks a few setup questions. After that:

> Use the blog-content-planner skill for yoursite.com

### Recurring (every few days)

Create a scheduled task in Claude Cowork with a prompt like:

> Use the blog-content-planner skill for https://yoursite.com. Blog: https://yoursite.com/blog. Competitors: a.com, b.com. Audience: small business owners, plain language. Deliver a full draft and a thumbnail prompt.

Putting the profile in the task prompt is the most reliable option, because installed skill folders may be read-only in some environments and can't save a profile between runs.

## How it stores data

Per-site profile and topic log live in `blog-content-planner/references/projects/<site>/`. See `example-site/` for the format. One folder per site, so multiple products never mix.

## Customize

Edit `SKILL.md` to change the post length, structure, tone defaults, or thumbnail style.

## License

MIT
