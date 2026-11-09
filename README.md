# webview

Turn any pile of material (files, folders, globs, URLs, pasted text, images) into **one clean, structured web page**: a single self-contained `.html` file that opens in any browser, works offline, and can be sent to anyone.

Use it when you need to show a plan, proposal, set of findings, status update or set of docs to someone, without sending them a stack of Markdown files.

```
/webview docs/plan.md docs/adr/ screenshots/*.png
```

## How it works

1. **One quick question round.** It asks four multiple-choice questions at once, with recommended answers pre-picked from a glance at your material. Reply `go` to accept them.

   | Question | Options |
   | --- | --- |
   | **Goal:** what should the page help the reader do? | Understand · Decide · Catch up · Look up |
   | **Audience:** who's reading it? | Mixed team · Leadership & stakeholders · Engineers · Customers / end users |
   | **Depth:** how much time will they spend? | ~5 min · ~1 min · As long as it takes |
   | **Format:** what shape? | Auto · Document · Slides · Dashboard |

2. **No more questions.** It reads every source and reorganises the material for that reader. Content is grouped by theme, not by file. It uses tables, timelines and diagrams where they read faster, plus expandable depth, an "Open questions" callout and a "Sources" list. Every number, name, date and decision is kept exactly as written, and nothing is invented.
3. **A file.** It saves `~/webview/<name>.html` and opens it in your browser.

The page has no external requests, no vendor branding and no build step. It has light and dark themes, works on phones, and prints cleanly.

## Install

**Claude Code**

```
/plugin marketplace add prateekbisht23/webview
/plugin install webview@webview
```

**Other agents that support `SKILL.md` skills:** copy `skills/webview/` into that agent's skills directory. The skill uses no harness-specific tools. If the agent has no multiple-choice question UI, it asks the four questions as a numbered list instead.

## Develop locally

```
git clone https://github.com/prateekbisht23/webview
claude --plugin-dir ./webview
```

## Layout

```
.claude-plugin/
  plugin.json          plugin manifest
  marketplace.json     lets the repo act as its own marketplace
skills/webview/
  SKILL.md             the workflow
  SHAPING.md           how goal, audience and depth shape the outline
  DESIGN.md            visual system and the three formats
```

## License

MIT
