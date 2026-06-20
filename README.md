# Carousel Content Engine

A reusable instruction kit for generating branded, swipeable Instagram carousel content with AI.

This repo contains the operating rules, brand profile, and master carousel instructions used to create polished carousel concepts, self-contained HTML previews, captions, and export-ready PNG slides.

## What's Inside

| File | Purpose |
|---|---|
| `carousel-execution-rules.txt` | Highest-priority workflow rules for every carousel request. |
| `1. instagram-carousel-master-instructions.md` | Full carousel generation system: strategy, copy, design, HTML, captions, and export guidance. |
| `brand-profile.md` | Jason Building With AI brand identity, tone, colors, content pillars, and visual direction. |
| `carousel-3-ways-i-use-ai.html` | Example self-contained HTML carousel output. |
| `exports-3-ways-i-use-ai/` | Example PNG slide exports generated from the HTML carousel. |

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

Save the generated file with a descriptive name, for example:

```text
carousel-3-ways-i-use-ai.html
```

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

### 4. Publish Or Reuse

Use the exported PNG slides for Instagram, LinkedIn, X, or other social platforms. Keep the HTML file as the editable source version, and regenerate PNGs whenever you update copy or design.

## Showcase

Example carousel: **The 3 Ways I Actually Use AI**

The source HTML is included here: [`carousel-3-ways-i-use-ai.html`](carousel-3-ways-i-use-ai.html)

### Exported Slides

<p>
  <img src="exports-3-ways-i-use-ai/slide-01.png" width="220" alt="Slide 1">
  <img src="exports-3-ways-i-use-ai/slide-02.png" width="220" alt="Slide 2">
  <img src="exports-3-ways-i-use-ai/slide-03.png" width="220" alt="Slide 3">
</p>

<p>
  <img src="exports-3-ways-i-use-ai/slide-04.png" width="220" alt="Slide 4">
  <img src="exports-3-ways-i-use-ai/slide-05.png" width="220" alt="Slide 5">
  <img src="exports-3-ways-i-use-ai/slide-06.png" width="220" alt="Slide 6">
</p>

<p>
  <img src="exports-3-ways-i-use-ai/slide-07.png" width="220" alt="Slide 7">
</p>

## Recommended Workflow

1. Pick one topic and one clear objective.
2. Use the execution rules, master instructions, and brand profile as context.
3. Generate strategy and slide-by-slide copy first.
4. Generate the self-contained HTML carousel.
5. Review the HTML in a browser.
6. Export slides as PNGs.
7. Use the generated captions and hashtags when posting.

## Notes

GitHub README files do not support embedded interactive HTML previews, so this README showcases the generated PNG slides directly. Open the `.html` file locally if you want to inspect or edit the interactive carousel source.
