# Daily Knowledge Briefing — Routine

You run once each morning. Produce a first-principles learning briefing.

## Procedure

1. **Load state.** `cd` into the repo. Switch to the live branch that GitHub
   Pages serves: `git fetch origin claude/live && git checkout claude/live`.
   Read `seen.md` — never re-teach anything listed there.

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
   with the new briefing.

   The page is **calm, airy, light-only, full-width**: a 3×3 grid where each
   bucket is a column (tech / science / world), three cards per column, on a
   soft off-white background. Color appears only in the column headers and the
   本质/原理/意义 labels.

   **Change only these four things:**
   - the date in `<title>`
   - the date in `<div class="sub">`
   - the `Nº` counter in `<span class="sig">`
   - the nine `<article class="item">` blocks

   Everything else is the design — copy it through byte for byte. Specifically:

   - Keep `<meta charset="utf-8">` and `<meta name="viewport" ...>`. Without the
     charset the 本质/原理/意义 labels turn to mojibake.
   - Keep the entire `<style>` block untouched. Do not add a dark mode.
   - Keep the DOM structure exactly: `.wrap` contains `header.mast`, then three
     `section.sec` with `data-b="tech" | "sci" | "world"`, then `footer`. The
     three sections ARE the three grid columns — do not merge, reorder, or add
     one, and keep exactly three `article.item` per section.
   - Each section opens with `<div class="sec-head"><h2>NAME</h2><span class="rule"></span></div>`.
     The `span.rule` is the colored bar. Do not drop it.
   - Each beat is
     `<div class="beat"><div class="lab">本质<small>What it is</small></div><p>…</p></div>`,
     with the three labels in order: 本质 / 原理 / 意义 and the small tags
     "What it is" / "The principle" / "Why it matters".
   - In each 原理 beat, wrap the single most important phrase in `<em>` — it
     renders as the accent color, and it is the one thing the reader should
     take away.

   Card headlines run 6–12 words; the columns are narrow, so a long headline
   wraps to three lines and looks cramped.

7. **Persist + push (REQUIRED).** Write `briefings/YYYY-MM-DD.md` (markdown),
   append the 9 identifiers to `seen.md` (prune >30 days), then
   `git add -A && git commit -m "Briefing YYYY-MM-DD" && git push origin claude/live`.
   You are on the `claude/live` branch (routines may push to `claude/*` by
   default). The push to `claude/live` is what refreshes the live page at
   **https://mimiai-dev.github.io/knowledge/** — it must succeed.

No email. The live page is the sole delivery channel.
