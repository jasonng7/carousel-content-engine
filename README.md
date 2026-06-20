# Carousel Content Engine

A reusable instruction kit for generating branded, swipeable Instagram carousel content with AI.

This repo contains the operating rules, brand profile, and master carousel instructions used to create polished carousel concepts, self-contained HTML previews, captions, and export-ready PNG slides.

Generated HTML and PNG files are local working outputs. They are intentionally not committed to this repo.

## What's Inside

| File | Purpose |
|---|---|
| `carousel-execution-rules.txt` | Highest-priority workflow rules for every carousel request. |
| `1. instagram-carousel-master-instructions.md` | Full carousel generation system: strategy, copy, design, HTML, captions, and export guidance. |
| `brand-profile.md` | Jason Building With AI brand identity, tone, colors, content pillars, and visual direction. |
| `carousel-*.html` | Local generated HTML carousel files. Ignored by Git. |
| `exports*/` | Local exported PNG slide folders. Ignored by Git. |

## How To Use This Repo

Use the three instruction files as the source of truth whenever you ask an AI assistant to create a carousel.

### 1. Start With The Instruction Files

Give your AI assistant these files:

1. `carousel-execution-rules.txt`
2. `1. instagram-carousel-master-instructions.md`
3. `brand-profile.md`

Then ask for a carousel using a simple request like:

```text
Using the uploaded carousel execution rules, master instructions, and brand profile, create an Instagram carousel about:

Topic: 3 ways I actually use AI in my daily business workflow
Goal: Educate business owners and creators
Audience: AI-curious founders, creators, and solopreneurs
CTA: Follow @jason.bwai for practical AI workflows

Please generate:
- carousel strategy
- slide-by-slide copy
- self-contained HTML carousel
- short Instagram caption
- long Instagram caption
- hashtags
```

### 2. Generate The HTML Carousel

Ask the AI assistant to output a single self-contained `.html` file that includes:

- HTML
- CSS
- JavaScript
- carousel navigation
- swipe support
- keyboard navigation
- Instagram-style preview frame
- export-ready slide containers

Save the generated file locally with a descriptive name, for example:

```text
carousel-3-ways-i-use-ai.html
```

Generated HTML files are treated as local working files and are ignored by Git.

### 3. Export PNG Slides

Ask the AI assistant to generate a Playwright export script for the HTML carousel, or use your preferred browser screenshot workflow.

Recommended export format:

- slide size: `1080 x 1350 px`
- file naming: `slide-01.png`, `slide-02.png`, etc.
- output folder: `exports-[carousel-name]/`

Example:

```text
exports-3-ways-i-use-ai/
  slide-01.png
  slide-02.png
  slide-03.png
  slide-04.png
  slide-05.png
  slide-06.png
  slide-07.png
```

Generated PNG export folders are also treated as local working outputs and are ignored by Git.

### 4. Preview Locally

Open the generated HTML file in your browser to preview the carousel interface.

You can also view exported slides locally after export:

```text
exports-3-ways-i-use-ai/
  slide-01.png
  slide-02.png
  slide-03.png
  slide-04.png
  slide-05.png
  slide-06.png
  slide-07.png
```

This gives you the same slide-grid preview style locally without uploading generated PNG files to GitHub.

### 5. Publish Or Reuse

Use the exported PNG slides for Instagram, LinkedIn, X, or other social platforms. Keep the HTML file as the editable source version, and regenerate PNGs whenever you update copy or design.

## Showcase

Example carousel: **The 3 Ways I Actually Use AI**

The example output is kept local instead of being uploaded to the repo:

- `carousel-3-ways-i-use-ai.html`
- `exports-3-ways-i-use-ai/slide-01.png` through `slide-07.png`

Open the HTML file locally to see the interactive preview, or open the export folder to see the PNG slide grid.

## Recommended Workflow

1. Pick one topic and one clear objective.
2. Use the execution rules, master instructions, and brand profile as context.
3. Generate strategy and slide-by-slide copy first.
4. Generate the self-contained HTML carousel.
5. Review the HTML in a browser.
6. Export slides as PNGs.
7. Use the generated captions and hashtags when posting.

## Notes

GitHub README files do not support embedded local-only HTML or PNG previews. This repo keeps generated `.html` and `.png` outputs local by default, so GitHub only stores the reusable instruction system.
