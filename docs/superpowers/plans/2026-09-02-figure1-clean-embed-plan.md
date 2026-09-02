# Figure 1 Clean Embed Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make the public Figure 1 embed show only a clean, enlarged chart with no surrounding copy or caption.

**Architecture:** Keep the existing chart renderer and data unchanged. Apply embed-entrypoint-only CSS to hide non-chart content, remove the chart heading and caption, and enlarge SVG text classes without changing chart geometry or hover behavior.

**Tech Stack:** Standalone HTML, CSS, inline JavaScript, SVG, GitHub repository, HTML preview proxy.

## Global Constraints

- Only `figure1.html` changes visually; `index.html` remains the complete figure set.
- Preserve existing Figure 1 data, smoothing, colors, annotation, and hover tooltip behavior.
- Preserve responsive width and light/dark color behavior.
- Do not show page header, explanatory copy, title, subtitle, figure caption, or other figure sections.

---

### Task 1: Clean the Figure 1 embed surface

**Files:**
- Modify: `figure1.html` (embed-only style override at end of file)

**Interfaces:**
- Consumes: Existing `f1` chart mount and SVG classes (`.tick`, `.axname`, `.note`, `.note-strong`).
- Produces: A single visible Figure 1 chart frame suitable for Notion iframe embedding.

- [ ] **Step 1: Replace the embed override with the final visual rules**

Append a style override to `figure1.html` with these exact rules:

```html
<style>
  body { background: var(--surface); }
  .masthead,
  .plate:not(:first-of-type),
  .colophon,
  .plate-head,
  figcaption {
    display: none !important;
  }
  .wrap {
    max-width: 1120px;
    margin: 0 auto;
    padding: 0;
  }
  .plate:first-of-type {
    border-top: none;
    padding: 0;
  }
  .frame {
    border: 0;
    border-radius: 0;
    padding: 0;
    background: transparent;
  }
  .tick { font-size: 14px; }
  .axname { font-size: 14px; }
  .note { font-size: 15px; }
  .note-strong { font-size: 15px; }
</style>
```

- [ ] **Step 2: Verify the source contains no visible caption path**

Run:

```bash
rg -n "\.plate-head|figcaption|\.tick|\.axname|\.note-strong" figure1.html
```

Expected: the embed override hides `.plate-head` and `figcaption`, and the enlarged text rules are present.

- [ ] **Step 3: Commit the visual change**

```bash
git add figure1.html
git commit -m "Clean up Figure 1 embed presentation"
```

### Task 2: Publish and verify the public embed

**Files:**
- Publish: `figure1.html` from `main`

**Interfaces:**
- Consumes: GitHub `main` branch at `merak0514/RLRecipe`.
- Produces: `https://htmlpreview.github.io/?https://github.com/merak0514/RLRecipe/blob/main/figure1.html`

- [ ] **Step 1: Push the committed page**

```bash
git push origin main
```

Expected: the new commit is accepted on `main`.

- [ ] **Step 2: Verify visible content at the public URL**

Load the public URL in the browser and inspect the page. Expected: exactly one visible chart frame; no masthead, chart title, subtitle, caption, or Figure 2-4 content.

- [ ] **Step 3: Verify interaction and responsive text**

At desktop width, move the pointer over the chart plot. Expected: the vertical guide, highlighted point, and tooltip still appear. At a narrow viewport, expected: the enlarged axis labels and annotation remain inside the chart without horizontal overflow.
