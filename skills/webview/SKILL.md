---
name: webview
description: Turn files, folders, pasted docs or images into one clean, self-contained web page you can open anywhere or send to anyone.
disable-model-invocation: true
argument-hint: <files | folders | globs | URLs | pasted text>
---

# /webview

Turn whatever the user handed over into a single **presentable** web page (structured, calm, easy to skim), saved as one self-contained HTML file. The page must let someone grasp the material faster than reading the sources.

The output is **portable**: one `.html` file that works offline in any browser, with no build step, no server, no account and no external requests. The person receiving it needs nothing but the file.

The source material is: $ARGUMENTS
Anything pasted or attached alongside the command counts as source too.

The run has exactly one interruption: the brief in step 1. After it, work **silently** through to the finished file. Resolve every later ambiguity yourself with the most sensible default, and note the call in the final reply.

## 1. Brief: one question round

If nothing was provided, ask for the material and stop.

Otherwise, take a **glance** (file names, titles, first headings; nothing deeper) so you can mark the best-fitting option on each question as recommended. Then ask all four questions at once. Use the harness's structured multiple-choice question tool if it has one. If it doesn't, send a single message that lists the questions numbered with lettered options, marks the recommended ones, and ends with: *Reply like `1a 2c 3a 4a`, or just `go` for the recommended set.*

**1. Goal: what should this page help the reader do?**
- **Understand**: explain what it is and how it works (onboarding, explainers, overviews)
- **Decide**: get a review or sign-off (plans, proposals, RFCs, options with trade-offs)
- **Catch up**: report what happened (status updates, findings, audits, incidents, research results)
- **Look up**: a reference to come back to (docs, specs, runbooks, handbooks)

**2. Audience: who's reading it?**
- **Mixed team**: plain language, with technical detail tucked into expandable sections
- **Leadership & stakeholders**: outcomes, decisions, risks and cost; minimal implementation
- **Engineers**: architecture, interfaces, code, edge cases
- **Customers / end users**: benefits and how-to, no internals

**3. Depth: how much time will they spend?**
- **~5 minutes**: key points with supporting detail
- **~1 minute**: the gist, decisions and next steps only
- **As long as it takes**: everything preserved, organised for lookup

**4. Format: what shape should it take?**
- **Auto**: best fit for the goal and material
- **Document**: scrolling page with sidebar navigation
- **Slides**: one idea per screen, arrow keys to move; for presenting live
- **Dashboard**: cards, metrics and status at a glance

Done when: all four answers are in hand, either chosen or accepted as recommended.

## 2. Ingest

Read every source in full:

- **Files**: Markdown, code, PDFs, notebooks, CSV/JSON, images (look at them).
- **Folders and globs**: walk them recursively. Skip `.git`, `node_modules`, build output, lockfiles and binaries. When a folder has more than ~40 relevant files, read the READMEs, docs and entry points in full and skim the rest.
- **URLs**: fetch them.
- **Pasted text**: treat it as a document of its own.

Done when: every source is accounted for, either read or deliberately skipped with a reason. Keep that inventory, because the page's "Sources" section is built from it.

## 3. Shape

Read [SHAPING.md](SHAPING.md) and build the outline from the chosen goal, audience and depth. You are re-architecting the material for its reader, not concatenating files in order:

- Open with what the reader needs first: the gist in 2–4 sentences, plus key facts or decisions as scannable tiles.
- Group by **theme**, not by source file. Merge overlapping content and keep each fact in one place.
- Turn the material into the forms that read fastest: comparisons become tables, sequences become numbered steps or timelines, architecture and flows become diagrams, status becomes badges, and long tangents go into expandable sections.
- Keep **fidelity**: every number, name, date, decision and open question survives exactly as the source states it. Never invent content. Flag gaps and contradictions in an "Open questions" callout.
- Close with "Sources", listing each input and what it contributed.

Done when: every outline section maps to source material, and every important source point has a place in the outline.

## 4. Build

Write the page following [DESIGN.md](DESIGN.md). Save it as `~/webview/<slug>.html` (create the folder if needed), where `<slug>` is a short kebab-case name derived from the content. If that file already exists, add a numeric suffix rather than overwriting it. Open it in the default browser (`open` on macOS, `xdg-open` on Linux, `start` on Windows).

Done when: the file opens, every outline section is present and populated, and the page makes no network requests.

## 5. Hand back

Reply with:

- the absolute file path on its own line,
- one line on the goal, audience, depth and format used,
- any calls you made silently (skipped sources, assumptions, contradictions found).

Nothing else.
