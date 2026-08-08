# Publish August 8 Briefing Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the verified August 8, 2026 briefing to the existing GitHub Pages site and archive it in Markdown.

**Architecture:** Preserve the static single-page site and its three-column design. Update `index.html` with nine source-linked items and create a matching dated Markdown archive.

**Tech Stack:** Static HTML/CSS, Markdown, GitHub Pages.

## Global Constraints

- Exactly nine items: three Edge Tech, three Science, and three World.
- Each item explains what happened, its underlying principle, and why it matters.
- Every item links to its direct source.
- No new dependencies or site redesign.

---

### Task 1: Publish and archive the briefing

**Files:**
- Modify: `index.html`
- Create: `briefings/2026-08-08.md`

- [x] Replace the homepage content and date while retaining the responsive three-column design.
- [x] Add the same nine stories to the dated Markdown archive.
- [x] Validate HTML structure, item counts, dates, and outbound links.
- [x] Prepare the verified change for commit and push to `origin/main`.
