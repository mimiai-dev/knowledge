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

6. **Publish the live page (REQUIRED).** Overwrite `index.html` in the repo root
   with the new briefing: dated title, three sections (Tech / Science / World),
   9 items, light/dark aware, source links. Keep the existing `index.html`'s
   visual design (tokens, layout, 本质/原理/意义 three-beat) — replace only the
   content.

7. **Persist + push (REQUIRED).** Write `briefings/YYYY-MM-DD.md` (markdown),
   append the 9 identifiers to `seen.md` (prune >30 days), then
   `git add -A && git commit -m "Briefing YYYY-MM-DD" && git push`. The push is
   what refreshes the live page at **https://monistdavid.github.io/knowledge/**
   and the archive — it must succeed. (Requires the repo's GitHub write access to
   be connected to the cloud environment.)

No email. The live page is the sole delivery channel.
