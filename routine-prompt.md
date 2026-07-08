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
   - World news: reputable outlets that the search crawler can actually reach —
     NPR, Al Jazeera, France 24 (all verified accessible). NOTE: Reuters, AP,
     AFP, BBC, The Guardian, DW, Ars Technica, and The Verge BLOCK the crawler —
     do not put them in `allowed_domains` or the WebSearch call fails entirely.
     Corroborate across the accessible outlets instead.

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

6. **Compose the page.** Build the briefing as a full HTML document: dated
   title, three sections (Tech / Science / World), 9 items, light/dark aware,
   source links. Keep the same visual design as the existing `index.html` —
   replace only the content. Save it as `index.html` in the repo root.

7. **Deliver by email (PRIMARY — this is the deliverable).** Email the user
   (mimi.ai.system@gmail.com) via the Gmail connector. Send the FULL briefing as
   the HTML body (the email itself is the readable page), subject
   `Daily Knowledge Briefing — YYYY-MM-DD`. This step is REQUIRED and must
   succeed; the email is how the user actually receives the briefing.

8. **Persist to git (BEST-EFFORT — do not block on it).** Also write
   `briefings/YYYY-MM-DD.md` (markdown), append the 9 identifiers to `seen.md`
   (prune >30 days), then try `git add -A && git commit -m "Briefing YYYY-MM-DD"
   && git push`. If the push fails (no write credential), log it and continue —
   the email already delivered. When GitHub write access is connected, this also
   updates the archive, dedup state, and the live page at
   https://monistdavid.github.io/knowledge/.

**Dedup note:** read `seen.md` if present. If the git push has not been working
(seen.md looks stale), lean on the ~24h freshness window and your own judgment to
avoid repeats, since persistent state may be unavailable until write access is set up.
