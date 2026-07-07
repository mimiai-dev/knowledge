# Daily Knowledge Briefing — Design

**Date:** 2026-07-07
**Owner:** monistdavid (mimi.ai.system@gmail.com)
**Status:** Approved design, pre-implementation

## Purpose

A personal learning tool. Every morning at 9am it researches the frontier of
technology, science, and world affairs, then teaches the 9 most significant new
things from first principles (第一性原理) — not news blurbs, mini-lessons. The
goal is that the user learns something real every day.

## Decisions (locked)

| Decision | Choice |
|---|---|
| Delivery | Web page (Artifact), stable URL bookmarked once, refreshed daily |
| Depth | Focused; each item explained from first principles |
| Volume | 9 items: 3 edge-tech / 3 science / 3 world news |
| Engine | Scheduled cloud routine, cron `0 9 * * *` America/New_York |
| Archive | Git-backed: private GitHub repo, routine commits daily |
| Notification | Stable Artifact URL + best-effort email nudge |

## Architecture

```
9am cron (cloud routine)
  → 1. Load state   (git pull; read seen.md)
  → 2. Gather       (WebSearch across tiered source allowlist, last ~24h)
  → 3. Verify       (corroboration gate; drop unverifiable)
  → 4. Select       (3 most significant new items per bucket)
  → 5. Teach        (first-principles write-up per item)
  → 6. Publish       (update stable Artifact web page)
  → 7. Persist      (write briefings/YYYY-MM-DD.md, update seen.md, commit+push)
  → 8. Notify       (best-effort email with the link)
```

The routine runs against the GitHub repo. Local `/Desktop/Knowledge` stays in
sync via `git pull`. The routine's cloud checkout is the write path; the local
folder is a read replica.

## Run steps in detail

**1. Load state.** `git pull`. Read `seen.md` (rolling ~30-day list of covered
item identifiers) so nothing gets re-taught.

**2. Gather.** WebSearch per bucket, restricted to the source allowlist below,
filtered to roughly the last 24 hours.

**3. Verify (reliability layer).** Hard rules, baked into the routine prompt:
- **Link the primary source, not the coverage** — arXiv paper over the blog
  about it; the company post over the rumor; the wire report over the aggregator.
- **Corroboration gate** — a news/science claim needs a primary source OR ≥2
  independent reputable sources. Fails → dropped, or included only if explicitly
  labeled "unconfirmed."
- **Denylist** — no social-media rumor, no clickbait/SEO farms, no
  single-anonymous-source stories, no press releases dressed as findings.

**4. Select.** The 3 most significant *new* (not in `seen.md`) items per bucket.
Significance over sensationalism.

**5. Teach.** Each item written 第一性原理-style:
what it is → the underlying principle/mechanism → why it matters. Plus its
source link. Aim for genuine understanding, not summary.

**6. Publish.** Update ONE Artifact in place (stable URL). Page: dated title,
three sections (Tech / Science / World), 9 items with source links. Light/dark
aware.

**7. Persist.** Write `briefings/YYYY-MM-DD.md` (the same content, markdown),
append the day's item identifiers to `seen.md` (prune entries >30 days),
`git commit && git push`.

**8. Notify.** Best-effort email to the user with the stable link + today's 9
headlines. If Gmail is unavailable in the headless run, skip silently — the
bookmarked URL is the reliable channel.

## Source allowlist

- **Tech:** arXiv (cs.*), official company engineering blogs, GitHub, Hacker
  News *as a pointer to primary sources only*, established hardware/tech press.
- **Science:** arXiv, peer-reviewed journals (Nature, Science, Cell, PRL…),
  university/lab press releases, Quanta.
- **World news:** wire services & papers of record only — Reuters, AP, AFP, BBC,
  plus 1–2 regional papers of record for context.

## Repo layout

```
/Desktop/Knowledge/
  README.md
  seen.md                     # rolling ~30-day dedup state
  briefings/
    2026-07-07.md             # per-day archive
  docs/superpowers/specs/
    2026-07-07-daily-knowledge-briefing-design.md
  routine-prompt.md           # the exact prompt the cloud routine runs
```

## State files

- `seen.md` — list of covered item identifiers with dates; dedup + freshness.
- `briefings/YYYY-MM-DD.md` — permanent per-day archive.
- `routine-prompt.md` — source of truth for what the routine does; the schedule
  routine references/embeds this.

## Out of scope (YAGNI)

- Personalization / topic weighting beyond the fixed 3/3/3.
- Interactive UI, search over archive (git grep suffices).
- Multiple languages of delivery (explanations may use 第一性原理 framing; page is
  otherwise English).
- Push/mobile app notifications beyond the email nudge.

## Open risks

- **Artifact publishing from a headless routine** is the main technical unknown;
  if it can't publish, fallback is committing a rendered HTML to the repo +
  GitHub Pages. Validate early.
- **Gmail in headless runs** may be absent (expected); email is best-effort only.
