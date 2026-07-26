---
name: Upwork Portfolio Item
description: Creates portfolio visuals (cover image + demo screenshot) and copy (title, description, skill tags) for adding a shipped project to the Upwork portfolio. Use when the user wants to add a project to Upwork, needs portfolio images, or asks for portfolio copy.
---

# Upwork Portfolio Item

Produces everything needed to add one finished project to the Upwork portfolio: a cover image, an optional second "proof it works" image, and the title/description/skill-tag copy.

## Images

Two images, different jobs:

### 1. Cover image — square, not a crop of a wide banner
Upwork's portfolio grid crops the cover into a near-square thumbnail. **Design it square from the start (1200x1200, then downscale to 800x800 final)** — don't reuse a wide 4:1 README-style banner and let Upwork crop it. A wide banner center-cropped to square loses the icon/logo off the edge and leaves the text floating oddly.

Composition that works: dark background with subtle grid + radial glow, icon/logo centered near the top, project name below it (large, bold, monospace), one-line subtitle below that, then a small list of key features/tools at the bottom (muted, small monospace). Everything centered, self-contained — assume it might get cropped from any edge.

Final size: **800x800px**. Render larger (1200x1200) for crispness, then `sips --resampleHeightWidth 800 800 file.png` to downscale.

### 2. Demo/proof image (optional but strong) — real data, not fabricated
A styled "product shot" showing the thing actually working — a chat/terminal-style card with macOS traffic-light window chrome, showing a real user question, a real tool call, and the **actual real output** (copy it from a real test run in the session, don't make up numbers). This is more convincing than a static logo because it proves the software runs.

Size to the content — don't guess a big canvas and leave dead space below. Render once, check the screenshot, adjust the HTML `height` to match actual content height, re-render.

## Rendering method

**Use headless Chrome, not `qlmanage`.** `qlmanage -t` (macOS Quick Look thumbnails) gives unreliable, inconsistent scaling/padding for SVG. If no `rsvg-convert`/`inkscape`/`cairosvg` is installed, render via headless Chrome instead:

1. Write the visual as an HTML file with inline `<style>` (or wrap an existing SVG in an `<img>` sized via CSS)
2. Set `html, body { width: <W>px; height: <H>px; }` to match the exact target canvas
3. Render:
   ```
   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
     --headless --disable-gpu \
     --screenshot=/path/out.png \
     --window-size=<W>,<H> \
     --force-device-scale-factor=1 \
     --hide-scrollbars \
     "file:///path/to/file.html"
   ```
4. Read the resulting PNG back to visually verify before finalizing — don't ship unseen
5. Clean up temp HTML/intermediate PNGs afterward

## Visual style — suggested default, swap for your own brand

A dark/understated palette that reads well and isn't loud. Treat these as a starting point, not a rule — swap in your own brand colors if you have them.

- Background: `#0a0d0a` (near-black, not pure black)
- Bright accent: pick one color for headline highlights, checkmarks, key numbers
- Supporting tones: two darker/muted shades of the same accent for icons, borders, less prominent elements
- Primary text: `#f1f5f4` / `#e5e7eb` (off-white, not pure white)
- Secondary/muted text: `#9ca3a3`, `#6b7280`, `#4b5563` (descending emphasis)
- Subtle grid background (`linear-gradient` lines, ~28-32px cells, `#1f2937`, opacity ~0.35) + a soft radial glow in the accent color for texture — don't leave the background flat
- Monospace (`ui-monospace, Menlo, 'SF Mono', monospace`) for anything code/tool/CLI-related; system sans-serif for prose/UI text
- Simple line-art icon relevant to what the project does — not a stock icon, not overly detailed

## Where files live

Portfolio/marketing images belong with your private dev work, never in a public GitHub repo (e.g. `<project>-private/assets/upwork/` if you keep a private dev copy alongside a published public one). The public repo only gets the project's own README banner — Upwork-specific marketing assets aren't part of the open-source project.

## Copy pattern

**Title:** `<Project Name> — <positioning tagline>` — e.g. "Acme Inventory Sync — Real-Time Warehouse Data Tool"

**Description** — Upwork caps this field at **600 characters**. Count before finalizing (`python3 -c "print(len(open('desc.txt').read()))"` or similar) — don't write a full-length draft and hand it over assuming it fits, it won't. Three short paragraphs, compressed to fit the cap:
1. What it does + who it's for, one or two sentences
2. Live links — npm package, GitHub repo (proof it's real and shipped, not a mockup)
3. Tech stack + quality signals (validated inputs, error handling, tested against the live API, clean architecture) — this is what separates a portfolio piece from a tutorial project

**Skill tags:** prefer specific over generic. Include the actual protocol/technology name if it's the point of the project (e.g. `MCP`, not just `API Integration`). Drop tags that add no signal because they're implied by another tag already selected (e.g. don't list both `TypeScript` and `Node.js` — pick the more specific one for the context).

**Your Role** — Upwork caps this field at **100 characters**. Solo projects: one line, comma-separated list of what you actually did (architecture, implementation, testing, release), not a narrative paragraph. Count it the same way as the description.
