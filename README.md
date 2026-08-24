# AI and Facilities

Slides for **WLCG Open Technical Forum #12** ("AI-driven Evolution in WLCG", CERN,
25 August 2026) by Rob Gardner, Giordon Stark, Ilija Vukotic, and Fengping Hu (University
of Chicago): *"AI and Facilities — towards trustworthy adoption of agentic management and use."*

**▶ View the deck:** https://robrwg.github.io/2026-08-25-WLCG-OTF12/

Two trust problems, one facility: AI acting **on** the facility (privileged actions a
sysadmin would do — earned incrementally through runbooks, governance levels, reviewable
memory, and dual enforcement) and AI acting **through** it (a physicist's analysis, driven
from their laptop via a credential-brokered MCP gateway, the "USB-C port" of the analysis
facility). Grounded in what runs today at the UChicago ATLAS Analysis Facility, and framed
as options for what WLCG could — or need not — coordinate.

Rebuilt from Giordon Stark's Nikhef colloquium deck
([kratsg/2026-07-01-nikhef-colloquium](https://github.com/kratsg/2026-07-01-nikhef-colloquium)),
which carries the physicist-side story in full.

## What's here

| Path | What it is |
|------|------------|
| `presentation.html` | The deck (reveal.js 6.0.1, loaded from CDN — no build step) |
| `styles.css` | UChicago-maroon theme (CSS variables, `pt` font sizing) |
| `images/` | Committed figures, the demo video, and the hand-authored `NEW-*.svg` diagrams |
| `.agents/skills/` | The `revealjs` build skill + `grill-me`, used to author the deck |
| `.github/workflows/deploy.yml` | Auto-publishes to GitHub Pages on push to `main` |

## Structure

Vision-first and **layered**: a broad main line any physicist can follow, with optional
technical **deep-dive / backup** slides (reachable by down-arrow in the vertical stacks).
Five sections: the thesis → an existence proof → the architecture that makes it portable →
the agenda of open problems → Nikhef, ESCAPE, and the discussion.

## View it

- **Online:** the GitHub Pages link above (always reflects `main`).
- **Locally:** open `presentation.html` in a browser. It pulls reveal.js from a CDN, so you
  need a network connection the first time.
- **Speaker notes:** press **`S`** in the browser (allow the popup) for speaker view —
  current + next slide, notes, and a timer. Every slide has notes.
- **Build stamp:** a small footer reads `dev` locally and `<short-sha> · <date>` on the
  deployed site, so you can tell which version is live.

## Edit it

Edit `presentation.html` directly (one slide / a few slides at a time), or use the in-browser
editor from the reveal.js skill:

```bash
node .agents/skills/revealjs/scripts/edit-html.js presentation.html
```

After editing, check for content overflow and review screenshots (Node deps live under
`.agents/skills/revealjs/node_modules`, gitignored — run `npm install` there if missing):

```bash
# flag any slide whose content exceeds 1280×720
node .agents/skills/revealjs/scripts/check-overflow.js presentation.html

# screenshot every slide (export mode disables animations)
.agents/skills/revealjs/node_modules/.bin/decktape reveal "presentation.html?export" \
  output.pdf --screenshots --screenshots-directory "screenshots/$(date +%Y%m%d_%H%M%S)"
```

> Heads-up: media-heavy slides (video / large images) can render *scaled-down* in the
> decktape export — that's a capture artifact. They render correctly in a real browser;
> trust `check-overflow.js` (it reports no overflow) over the decktape thumbnail.

## Deploy

Pushing to `main` triggers `.github/workflows/deploy.yml`, which publishes
`presentation.html` (as `index.html`) + `styles.css` + `images/` to GitHub Pages, injects the
build stamp, and attaches a best-effort `slides.pdf`. One-time setup: repo **Settings → Pages →
Source: GitHub Actions**.

## Credits

Slides AI-assisted by Claude (Anthropic). The title illustration is AI-generated; the
architecture (`NEW-af-mcp-arch.svg`) and pixi-pack (`NEW-pixi-pack.svg`) diagrams are
hand-authored. OpenWebUI / Slack screenshots and the Jupyter MCP video are real captures.
Built in the spirit of Gordon Watts' CHEP 2026 ecosystem framing.
