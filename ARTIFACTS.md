# Artifacts — Claude Code

This document explains what "artifacts" are in Claude Code and how to create, publish, and share them from a session.

## What is an artifact?
An artifact is a single static HTML or Markdown page that Claude Code publishes from your session to a private URL on claude.ai. The page can be interactive (HTML/CSS/JS inlined) and updates in pla[...]

Key points:
- Single file only: `.html`, `.htm`, or `.md`.
- No backend: artifacts are static; they cannot store form data or run server-side code.
- Live updates: republishing updates the page for all viewers.
- Connectors: artifacts may call MCP connectors (GitHub, databases, etc.) to fetch live data when a viewer opens the page.

## When to use an artifact
Use artifacts for output that is easier to view or interact with than to read as terminal text, such as:
- Annotated PR diffs and code walkthroughs
- Dashboards or charts summarizing data
- Design comparisons or mockups shown side-by-side
- Interactive controls for tuning parameters (sliders, toggles)
- Progress boards or investigation timelines that update while work runs

Do not use an artifact for a full hosted app or anything requiring a backend, authentication, or persistent server-side storage.

## Quick workflow
1. In Claude Code (CLI or desktop), ask Claude to make an artifact in plain language, e.g.:

   > Make an artifact that walks through PR #123 with the diff annotated inline.

2. Claude writes an HTML/Markdown file into the project and asks for permission to publish. Approve the publish prompt.
3. Claude publishes the page and prints/opens the private URL on claude.ai.
4. To update the page later, ask Claude to revise or republish the file (or republish as a long-running task proceeds).

## Using live data (connectors)
- If you want the artifact to fetch fresh data when a viewer opens it, tell Claude which connector to use in your prompt (for example, GitHub connector).
- When a viewer opens a connector-backed artifact, the page's connector calls run under the viewer's own connector account—so different viewers may see different data.
- The viewer must approve connector calls the first time; if they decline or lack a connector, the live sections remain empty. Include fallback text in those sections naming the connector required[...]
- Connector-backed artifacts cannot be shared publicly. They stay private to the publishing user or to organization members (depending on plan and settings).

## Sharing & collaboration
- Artifacts are private to the author by default. Use the page's Share control to add viewers or editors.
- On Team/Enterprise plans you can grant editors; editors republish by supplying the artifact URL to Claude in their own sessions.
- On Pro/Max plans you may publish a public link (connector-backed pages remain private).

## Constraints & limits (important)
- Plan & sign-in: publishing artifacts requires a supported plan (Pro/Max/Team/Enterprise) and a signed-in Claude session.
- File type & size: `.html`, `.htm`, or `.md`; rendered page must be under ~16 MiB.
- CSP: external network requests are blocked except Google Fonts and connector calls that run through claude.ai; images should be embedded as data URIs or use SVG.
- Claude Code version: artifacts require a sufficiently recent Claude Code or desktop version. If publishing fails, check CLI/app version and session authentication.

## Example prompts
- Annotated PR diff

  "Make an artifact that walks through PR #<PR_NUMBER> in this repository. Render the diff with inline annotations: for each changed hunk show a margin note with (a) purpose of change, (b) potenti[...]

- Dashboard with live data

  "Build an artifact dashboard of last week's deploy failures by service. Pull the live list through my GitHub connector when the page loads and include a refresh button. Include a fallback messag[...]

## Troubleshooting
- "Claude cannot publish": verify you are signed in and your plan/features allow artifacts; check the Claude Code version.
- Live sections empty for viewers: they may need to connect the connector, or they denied permission, or org admin disabled connector calls.
- Publish fails due to size: reduce embedded images, prefer SVG, or summarize large datasets rather than embedding them in full.

## Shared artifacts
- Public/Share link added by user on 2026-08-15:
  - https://claude.ai/public/artifacts/ef7ab2e5-be31-419e-b76d-675942ec5107  — Shared artifact URL provided by repository owner.

---
File created and maintained as a local guide to using Claude Code artifacts.
