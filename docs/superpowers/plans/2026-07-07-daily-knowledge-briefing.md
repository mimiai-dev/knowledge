# Daily Knowledge Briefing Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** A cloud routine that fires at 9am daily, researches tech/science/world-news from vetted sources, and publishes a first-principles web-page briefing of 9 items, archived to git.

**Architecture:** A scheduled cloud routine runs against the private `knowledge` GitHub repo. Each morning it reads `seen.md` for dedup, does verified WebSearch research, publishes/updates a stable Artifact web page, commits the day's archive back to the repo, and sends a best-effort email nudge. The `routine-prompt.md` file is the single source of truth for the daily behavior.

**Tech Stack:** Claude Code scheduled routines (cron), WebSearch, Artifact publishing, git/GitHub (`gh`), Gmail MCP (best-effort).

## Global Constraints

- Cron: `0 9 * * *`, timezone **America/New_York** (9am EDT/EST).
- Volume: exactly **9 items — 3 edge-tech / 3 science / 3 world news**.
- Teaching style: **first-principles (第一性原理)** — what it is → mechanism → why it matters.
- Sourcing: **allowlist only**; link the **primary** source; **corroboration gate** (primary source OR ≥2 independent reputable sources, else drop/label "unconfirmed"); **denylist** social rumor / clickbait / single-anonymous-source / PR-as-finding.
- Repo: `monistdavid/knowledge` (private). Commit author: `monistdavid <mimi.ai.system@gmail.com>`.
- One Artifact, updated in place → **stable URL**.

---

### Task 1: Repo scaffolding

**Files:**
- Create: `README.md`, `seen.md`, `.gitignore`, `briefings/.gitkeep`

- [ ] **Step 1: Write `.gitignore`**

```
.DS_Store
scratchpad/
```

- [ ] **Step 2: Write `seen.md`** (dedup state, starts empty with a header)

```markdown
# Seen items (rolling ~30-day dedup log)

Format: `YYYY-MM-DD | bucket | short-identifier`
```

- [ ] **Step 3: Write `README.md`**

```markdown
# knowledge

Personal daily learning briefing. A cloud routine runs at 9am America/New_York,
researches edge tech / science / world news from vetted sources, and teaches 9
items from first principles.

- Web page (stable Artifact URL): _added after Task 3_
- Archive: `briefings/YYYY-MM-DD.md`
- Daily behavior: `routine-prompt.md`
- Design: `docs/superpowers/specs/2026-07-07-daily-knowledge-briefing-design.md`
```

- [ ] **Step 4: Commit**

```bash
git add README.md seen.md .gitignore briefings/.gitkeep
git commit -m "Scaffold knowledge repo"
git push
```

---

### Task 2: Write `routine-prompt.md`

The exact instructions the cloud routine executes every morning. This IS the product.

**Files:**
- Create: `routine-prompt.md`

**Interfaces:**
- Produces: the daily procedure referenced by the scheduled routine (Task 5).

- [ ] **Step 1: Write `routine-prompt.md`** with the full daily procedure:

```markdown
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

7. **Persist.** Write `briefings/YYYY-MM-DD.md` (same content as markdown).
   Append the 9 item identifiers to `seen.md`; prune entries older than 30 days.
   `git commit -m "Briefing YYYY-MM-DD"` and `git push`.

8. **Notify (best-effort).** Email the user (mimi.ai.system@gmail.com) the
   stable link + the 9 headlines. If Gmail is unavailable, skip silently.
```

- [ ] **Step 2: Commit**

```bash
git add routine-prompt.md
git commit -m "Add daily routine prompt"
git push
```

---

### Task 3: Validation dry-run — produce today's briefing + publish Artifact

Prove the content quality AND the Artifact-publishing path (the flagged risk) by running one briefing manually in this session, following `routine-prompt.md` steps 2–6.

**Files:**
- Create: `briefings/2026-07-07.md` (in Task 4)

- [ ] **Step 1:** Execute research (step 2) + verify (step 3) for all 3 buckets using WebSearch, staying on the allowlist.

- [ ] **Step 2:** Select 9 items and write first-principles explanations (steps 4–5).

- [ ] **Step 3:** Write the page HTML to `scratchpad/briefing.html` and publish via Artifact (favicon `📡`, title `Daily Knowledge Briefing — 2026-07-07`).

- [ ] **Step 4:** Confirm the Artifact URL returned. **This is the risk gate** — if publishing works interactively, the routine path is sound. Record the URL.

- [ ] **Step 5:** Human check — is the briefing genuinely good (verified sources, real first-principles teaching, not blurbs)? Adjust `routine-prompt.md` if the output reveals prompt gaps.

---

### Task 4: Persist first briefing + wire the stable URL

**Files:**
- Create: `briefings/2026-07-07.md`
- Modify: `seen.md`, `README.md`

- [ ] **Step 1:** Write today's content to `briefings/2026-07-07.md` (markdown).
- [ ] **Step 2:** Append the 9 item identifiers to `seen.md`.
- [ ] **Step 3:** Put the stable Artifact URL into `README.md` (replacing the placeholder) and into `routine-prompt.md` step 6 so future runs update in place.
- [ ] **Step 4: Commit**

```bash
git add briefings/2026-07-07.md seen.md README.md routine-prompt.md
git commit -m "Briefing 2026-07-07 + wire stable artifact URL"
git push
```

---

### Task 5: Schedule the 9am cloud routine

**Files:** none (uses the schedule skill / routines).

- [ ] **Step 1:** Invoke the `schedule` skill to create a routine:
  - Schedule: `0 9 * * *` America/New_York
  - Repo: `monistdavid/knowledge`
  - Task: "Follow `routine-prompt.md` in the repo root exactly."
- [ ] **Step 2:** Confirm the routine is created and listed (schedule skill list / `CronList`).

---

### Task 6: Verify with a test fire

- [ ] **Step 1:** Trigger the routine once manually (schedule skill "run now" / `RemoteTrigger`).
- [ ] **Step 2:** Confirm it: pulled, produced 9 items, updated the SAME Artifact URL, committed a new `briefings/` file, updated `seen.md`, pushed.
- [ ] **Step 3:** If the headless run can't publish the Artifact, apply the fallback: render HTML into the repo + enable GitHub Pages for a stable URL, and update `routine-prompt.md` step 6 accordingly.
- [ ] **Step 4:** Confirm email nudge arrived (or confirmed absent → rely on bookmarked URL).

---

## Self-Review notes

- **Spec coverage:** delivery (Task 3/4/6), depth+first-principles (Task 2 step 5), 3/3/3 (Task 2 step 4), cloud engine (Task 5), git archive (Task 4), notification (Task 6), reliability layer (Task 2 step 3). All covered.
- **Risk:** Artifact-in-headless validated at Task 3 (interactive) and Task 6 (headless) with a concrete GitHub Pages fallback.
