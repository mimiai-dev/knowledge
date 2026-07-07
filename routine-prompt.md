# Daily Knowledge Briefing — Routine

You run once each morning. Produce a first-principles learning briefing.

## Procedure

1. **Load state.** `cd` into the repo, `git pull`. Read `seen.md` — never
   re-teach anything listed there.

2. **Research.** For each bucket, WebSearch for the most significant
   developments of the last ~24h. **Only** use these sources:
   - Tech: arXiv cs.*, official company engineering blogs, GitHub, Hacker News
     (as a pointer to primary sources only), established hardware/tech press.
   - Science: arXiv, peer-reviewed journals (Nature, Science, Cell, PRL…),
     university/lab press releases, Quanta.
   - World news: wire services & papers of record only — Reuters, AP, AFP, BBC,
     plus 1–2 regional papers of record.

3. **Verify (hard rules).**
   - Link the PRIMARY source, not the coverage.
   - Corroboration gate: a claim needs a primary source OR ≥2 independent
     reputable sources. Fails → drop it, or include only if labeled "unconfirmed".
   - Denylist: no social-media rumor, no clickbait/SEO farm, no
     single-anonymous-source story, no press release dressed as a finding.

4. **Select** exactly 9 NEW items (not in seen.md): 3 tech / 3 science / 3 world.
   Significance over sensationalism.

5. **Teach.** For each item write, from first principles (第一性原理):
   - **What it is** (plainly)
   - **The underlying principle/mechanism** (the real learning)
   - **Why it matters**
   - Source link (the primary one).

6. **Publish.** Update the SINGLE briefing Artifact IN PLACE (same URL — pass
   its `url`, find it via Artifact `action: list` if unknown). Page: dated
   title, three sections (Tech / Science / World), 9 items, light/dark aware.
   Stable URL: _added after first run_.

7. **Persist.** Write `briefings/YYYY-MM-DD.md` (same content as markdown).
   Append the 9 item identifiers to `seen.md`; prune entries older than 30 days.
   `git commit -m "Briefing YYYY-MM-DD"` and `git push`.

8. **Notify (best-effort).** Email the user (mimi.ai.system@gmail.com) the
   stable link + the 9 headlines. If Gmail is unavailable, skip silently.
