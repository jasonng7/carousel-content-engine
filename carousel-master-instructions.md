# Instagram Carousel Generator — Master Instructions
*The unified design system + build process for swipeable, export-ready IG carousels*

This file merges a process-oriented build guide with a proven, battle-tested design system (colors, type scale, component library, export pipeline) pulled from a working carousel. Use it end-to-end any time a carousel is requested.

The final output should feel like a polished Canva/Figma-style carousel, never a plain text slide deck.

---

## Core Goal

Every carousel request should produce:

1. Carousel content strategy (objective + narrative arc)
2. Slide-by-slide copy
3. A derived visual design system (colors, type, components)
4. A swipeable, self-contained HTML preview
5. Export-ready individual slide containers
6. A Playwright export script that turns slides into PNGs
7. An Instagram caption with hashtags and handle

---

## Step 1: Intake Checklist — Collect Before Building

Ask for anything missing before generating. Don't assume personal defaults unless the user explicitly says "you decide" — in that case, pick a clean, modern, high-contrast design and briefly state the assumptions before generating.

If the brand profile is blank, generic, or still contains placeholders, start with this brief onboarding interview in one concise message:

1. Who is the brand, creator, company, or campaign?
2. Who is the audience and what problem do they care about?
3. What tone, colors, visual references, or brand direction should guide the carousel?
4. What should the carousel achieve?
5. What is the topic and CTA?

Proceed once the answers are good enough to define a clear direction. Do not require perfect brand documentation before helping.

1. **Brand name** — shown on the first and last slides
2. **Instagram handle** — shown in the IG frame header and caption
3. **Primary brand color** — hex code, or a description to derive one from
4. **Logo** — SVG logo / uploaded image / brand initial / no logo
5. **Font pairing preference** — a style direction (see Step 4 table), or specific Google Fonts
6. **Tone** — professional, casual, playful, bold, minimal, educational, premium
7. **Topic / narrative** — what the carousel should teach, announce, or pitch
8. **Images/assets** — product images, profile photo, screenshots, background images, or none

If the user provides a website URL or brand assets, derive colors and typography direction from them instead of asking. If the user only says "make me a carousel about X" with no brand details, ask the onboarding questions first.

---

## Step 2: Define the Carousel Objective

Ask or infer the purpose — the whole carousel should be structured around **one** clear goal:

- Educate
- Sell
- Announce
- Explain a framework
- Share a tutorial
- Promote a product/service
- Build personal brand authority
- Drive traffic to a link
- Encourage comments, saves, or shares

---

## Step 3: Color System — Derive a Full Palette from One Primary

Never use random colors. Everything in the HTML traces back to the one brand color the user gave you.

```
BRAND_PRIMARY = {user's color}              // accent: progress bar, icons, tags
BRAND_DARK    = primary darkened ~30%        // CTA text, gradient anchor
BRAND_LIGHT   = primary lightened ~20%       // secondary accent: pills on dark, highlights
ACCENT        = optional secondary hue, used sparingly (rare stat highlight, alt tag)
LIGHT_BG      = warm or cool off-white       // never pure #fff
LIGHT_BORDER  = ~1 shade darker than LIGHT_BG
DARK_BG       = near-black, tinted to brand temperature
TEXT          = near-black on light slides / near-white on dark slides
MUTED_TEXT    = TEXT at ~40–60% opacity, for secondary copy
SURFACE/CARD  = LIGHT_BG or DARK_BG offset slightly, for cards and quote boxes
```

**Rules:**
- Warm primary → warm cream `LIGHT_BG`, warm-tinted `DARK_BG` (e.g. `#1A1918`)
- Cool primary → cool gray-white `LIGHT_BG`, cool-tinted `DARK_BG` (e.g. `#0F172A`)
- Brand gradient (used on "solution"/"CTA" slides):
  `linear-gradient(165deg, BRAND_DARK 0%, BRAND_PRIMARY 50%, BRAND_LIGHT 100%)`
- Use the palette consistently across every slide — no off-system colors.

**Worked example (navy brand):**

| Token | Value |
|---|---|
| BRAND_PRIMARY | `#1B2B5B` |
| BRAND_DARK | `#0D1A38` |
| BRAND_LIGHT | `#8BA3D4` |
| LIGHT_BG | `#F3F4F8` |
| LIGHT_BORDER | `#DDE0EA` |
| DARK_BG | `#0D1520` |

---

## Step 4: Typography System

Pick **one heading font** + **one body font** from Google Fonts based on tone:

| Style | Heading | Body |
|---|---|---|
| Editorial / premium | Playfair Display | DM Sans |
| Modern / clean | Plus Jakarta Sans (700) | Plus Jakarta Sans (400) |
| Warm / approachable | Lora | Nunito Sans |
| Technical / sharp | Space Grotesk | Space Grotesk |
| Bold / expressive | Fraunces | Outfit |
| Classic / trustworthy | Libre Baskerville | Work Sans |
| Rounded / friendly | Bricolage Grotesque | Bricolage Grotesque |

Apply via two CSS utility classes used everywhere: `.serif` (heading font) and `.sans` (body font). Never mix their roles — heading font = impact, body font = readability.

**Type scale.** Build the HTML at a 420 × 560px viewport (3:4) and export at 1080 × 1440px (scale factor ≈ **2.571** — see Step 5). The numbers below are build-width values; multiply by 2.571 for the equivalent exported pixel size.

| Role | Build width (420px) | Exported (1080px) | Notes |
|---|---|---|---|
| Hook / hero title | 30–38px | ~77–98px | Hero & CTA slides, weight 800, line-height 1.05–1.1 |
| Content slide heading | 32–34px | ~82–87px | Slides 2–6, weight 800, letter-spacing -0.4px |
| Section/tag label | 11px | ~28px | uppercase, letter-spacing 2.5px, weight 700, margin-bottom 14px |
| Bullet / body text | 15px | ~39px | line-height 1.5, weight 400 |
| Supporting/muted text | 13px | ~33px | line-height 1.45 |
| Overview card number | 28px | ~72px | weight 800, brand accent color |
| Overview card label | 15px | ~39px | weight 700 |
| Feature row label | 15px | ~39px | weight 700 |
| Feature row description | 13px | ~33px | weight 400, muted |
| CTA button text | 13px | ~33px | weight 700 |

Prioritize readability on mobile above all else.

---

## Step 5: Canvas & Export Dimensions — The Critical Technique

Default slide size: **1080 × 1440px (3:4 portrait)**. Only deviate if the user requests:

```text
1080 × 1080 px   square
1080 × 1350 px   4:5 portrait
1080 × 1920 px   story/reel
1920 × 1080 px   landscape
```

**Build and preview at 420 × 560px — never at 1080 × 1440px directly.** Export to full resolution by scaling, not by reflowing:

- Carousel viewport in the HTML = **420 × 560px**
- Export via Playwright's `device_scale_factor = 1080 / 420 ≈ 2.5714`
- **Never widen the viewport to 1080px to "export bigger."** Doing so reflows the entire layout — fonts shrink relative to their containers, spacing breaks, and the export no longer matches the preview the user approved.

This single rule is the difference between an export that matches the preview pixel-for-pixel and one that silently breaks.

---

## Step 6: Carousel Structure — Narrative Arc

Default to **7 slides**, alternating light/dark backgrounds for visual rhythm. Use 8–10 slides for longer topics. Not every topic needs every slide type below — adapt the sequence to the content, but keep one main idea per slide.

| # | Type | Background | Purpose |
|---|---|---|---|
| 1 | Hero | LIGHT_BG | Hook — bold claim, no description-y copy |
| 2 | Problem | DARK_BG | What's broken / outdated — use strikethrough pills |
| 3 | Solution | Brand gradient | The answer — quote/principle box |
| 4 | Features/Pillars | LIGHT_BG | What you get — icon + label + description rows |
| 5 | Proof/Details | DARK_BG | Stats, differentiators, big numbers |
| 6 | How-to | LIGHT_BG | Numbered steps, workflow |
| 7 | CTA | Brand gradient | Optional logo/handle, tagline, CTA button — **no arrow, 100% progress bar** |

**Rules:**
- Slide 1 must stop the scroll — lead with the value proposition, not a description.
- Last slide always ends on the brand gradient, full progress bar, no swipe arrow.
- Within this arc, vary the **layout style** per slide so the carousel doesn't feel like one template repeated — draw from: editorial card layout, big number + explanation, split image/text layout, framework diagram layout, checklist layout, quote/insight layout, CTA card layout. Keep components consistent (Step 9) even as layout varies.

---

## Step 7: Copywriting Rules

Write carousel copy that is short, punchy, easy to skim, mobile-first, and save-worthy.

- Maximum 35–45 words per slide
- Use strong hooks
- Use bold keywords
- Avoid long paragraphs
- Use numbered frameworks where helpful
- Make each slide understandable without explanation
- Use simple language

---

## Step 8: Required Elements & Layout Rules

Every slide must include:

- Clear main content area with strong visual hierarchy
- Consistent margins — standard content padding `0 36px`
- Slide number / progress indicator
- Optional footer or CTA
- Enough negative space

**Branding inside export slides:**
- Do not place a top brand header inside the slide canvas.
- Do not add a top-left logo/avatar plus brand name or a top-right handle on every slide.
- Do not let brand text compete with section labels, hooks, or headings.
- Keep brand identity in the color system, typography, caption, Instagram preview chrome, and final CTA slide.
- If a brand mark is needed before the final slide, use a tiny footer watermark only when it does not crowd the content.

**Progress bar (bottom, every slide):**
- Position: absolute bottom, `padding: 14–16px 28px 18–20px`
- Track: 3px height, rounded; fill width = `((index+1)/total) * 100%`
- Light slide: track `rgba(0,0,0,0.08)`, fill = BRAND_PRIMARY, label `rgba(0,0,0,0.3)`
- Dark/gradient slide: track `rgba(255,255,255,0.12)`, fill = `#fff`, label `rgba(255,255,255,0.4)`
- Counter label format: `"1/7"`, 11px, weight 500

**Swipe arrow (right edge, every slide EXCEPT the last):**
- Position: absolute right, full height, 48px wide, gradient fade background
- 24×24 chevron SVG, rounded stroke caps, stroke-width 2.5
- Light slide: bg `rgba(0,0,0,0.06)`, stroke `rgba(0,0,0,0.25)`
- Dark/gradient slide: bg `rgba(255,255,255,0.08)`, stroke `rgba(255,255,255,0.35)`
- **Omit entirely on the final slide** — its absence signals "end of carousel"

**Content placement:**
- All slides: `padding: 36px 0 52px` — top padding anchors content from the top; bottom padding clears the progress bar
- Hero / CTA slides: `justify-content: center; padding-top: 0` — vertically centred, no top padding
- Content slides (2–6): `justify-content: flex-start` — content flows from the top, filling downward naturally
- Do **not** use `justify-content: flex-end` — it creates empty space at the top and crowds content at the bottom
- Do **not** add decorative oversized numbers/glyphs in the corner — they add visual noise without adding value
- Content padding must always clear the progress bar — nothing overlaps interactive/UI zones

---

## Step 9: Reusable Component Library

Build these once and reuse identically across slides — repetition reads as intentional design.

- **Tag/category label** — uppercase, 11px, letter-spacing 2.5px, weight 700, margin-bottom 14px; color = BRAND_PRIMARY (light slides) / BRAND_LIGHT (dark slides) / `rgba(255,255,255,0.65)` (gradient slides)
- **Strikethrough pill** (problem slides) — `background: rgba(255,255,255,0.06); color: rgba(255,255,255,0.35); text-decoration: line-through`
- **Tag pill** (features/categories) — rounded pill, 11px weight 600, light = `rgba(BRAND_PRIMARY,0.08)` bg / dark = `rgba(BRAND_LIGHT,0.15)` bg
- **Overview card** (index/overview slides) — `border-radius: 14px; padding: 18px;` tinted border bg; number 28px weight 800 BRAND color; label 15px weight 700; gap between cards 14px; margin-top 20px
- **Bullet list row** — 15px weight 400, `padding: 9px 0`, with a subtle bottom border divider between items (`rgba(255,255,255,0.07)` on dark / `rgba(21,22,25,0.08)` on light); `margin-top: 16px`; last item has no border
- **Content angle / quote callout** — `border-left: 4px solid BRAND; padding: 14px 16px; border-radius: 0 10px 10px 0; margin-top: 20px;` with a tinted background (`rgba(BRAND,0.06–0.07)`); text 14px italic weight 600, line-height 1.5; replaces plain `border-left` lines
- **Feature row** — icon (44px rounded square, tinted bg, 20px SVG inside) + label (15px weight 700) + description (13px muted), bottom border divider; `padding: 14px 0`
- **Numbered step row** — large heading-font number (24px weight 300) + label (15px weight 700) + description (13px muted), bottom border divider
- **Big stat block** — number in heading font, 42–56px weight 300, label below in 12px uppercase muted; works well in a 3-column row separated by 1px dividers
- **CTA button** (final slide only) — pill button, `background: LIGHT_BG; color: BRAND_DARK`, 13px weight 700, `border-radius: 28px`, `padding: 11px 26px`

**Icon matching rule for feature rows:** never reuse one generic icon across all rows. Before drawing an icon, ask "what's the single object a reader would associate with this word in under a second?"

| Feature concept | Icon shape used |
|---|---|
| Calendar / scheduling / time | Clock face |
| Hooks / highlights / quality | Star |
| Engagement / replies / conversation | Speech bubble |
| Analytics / performance / growth | Bar chart |

Keep all icons in a row at the same stroke-width (2px), same size (20px inside a 44px container), and the same single accent color (BRAND_PRIMARY on light, white on dark) so the *set* feels designed even though each glyph differs. Mismatched or generic icons (e.g. four identical checkmarks) read as filler — the icon should help explain, not just decorate.

---

## Step 10: Image Usage Rules

If images are provided:
- Use them intentionally, not decoratively; crop cleanly; never stretch
- Use rounded corners or framed cards; keep text readable over images (add subtle overlays if needed)
- Place images where they support the message
- **Embed all images as base64 data URIs directly in the HTML** — the file must stay fully self-contained
- If an uploaded image renders broken, check its actual format with `file` and use the matching `data:image/...` prefix

If no images are provided, use shapes, cards, gradients, icons, numbers, lines, and visual hierarchy instead. Never use fake logos or copyrighted brand assets unless the user provided them.

---

## Step 11: Instagram Frame (Preview Wrapper)

Wrap the carousel in IG chrome for in-chat preview only — this gets stripped before export:

- Header: avatar circle (BRAND_PRIMARY bg, initial or icon) + handle + subtitle
- Viewport: 420×525px, draggable/swipeable track
- Dot indicators below the viewport (active dot = pill-shaped, BRAND_PRIMARY)
- Action row: heart / comment / share / bookmark SVG icons
- Caption: handle + 1-line description + timestamp

The interactive preview must let the user:
- Swipe or drag through slides
- Click next/previous buttons
- See slide numbers
- Navigate by keyboard (arrow keys)
- Check the full design before exporting

---

## Step 12: HTML Output Requirements

Generate one fully self-contained HTML file with HTML, CSS, and JavaScript — it must work by simply opening the file in a browser, with no external build tools. Google Fonts may be imported.

It must include: swipe/drag navigation, next/previous controls, slide dots or progress bar, keyboard navigation, the responsive IG-frame preview wrapper, and fixed-size export-ready slide containers.

Each slide is its own `.slide` element with fixed dimensions:

```html
<section class="slide" data-slide="1">
  ...
</section>
```

**Build notes:**
- Generate the HTML with Python (`Path.write_text()`), never via shell variable interpolation — `$`, backticks, and bare numbers get corrupted in shell heredocs.
- Avoid animations inside the export area that could affect screenshots.

---

## Step 13: Export Pipeline — Playwright Script (1080×1350 PNGs)

Always generate this when the user asks for image export. Reuse and adapt an existing export script if the project already has one.

**Critical rules:**
1. Keep the viewport at **420×525** and scale via `device_scale_factor` — never widen it to 1080px (see Step 5)
2. Wait for fonts and images to load before screenshotting
3. Hide all IG-chrome elements before capturing
4. Screenshot each `.slide` individually, saved as `slide-01.png`, `slide-02.png`, etc.

```python
import asyncio
from pathlib import Path
from playwright.async_api import async_playwright

INPUT_HTML = Path("/path/to/carousel.html")
OUTPUT_DIR = Path("/path/to/exports")
OUTPUT_DIR.mkdir(exist_ok=True)
TOTAL_SLIDES = 7

VIEW_W = 420
VIEW_H = 560          # 3:4 default (change to 525 for 4:5, 420 for square)
SCALE = 1080 / 420   # ≈ 2.5714  →  exports at 1080×1440 px

async def export_slides():
    async with async_playwright() as p:
        browser = await p.chromium.launch()
        page = await browser.new_page(
            viewport={"width": VIEW_W, "height": VIEW_H},
            device_scale_factor=SCALE,
        )
        html_content = INPUT_HTML.read_text(encoding="utf-8")
        await page.set_content(html_content, wait_until="networkidle")
        await page.wait_for_timeout(3000)  # let Google Fonts load

        # Strip IG chrome, isolate the slide viewport
        await page.evaluate("""() => {
            document.querySelectorAll('.ig-header,.ig-dots,.ig-actions,.ig-caption')
                .forEach(el => el.style.display = 'none');
            const frame = document.querySelector('.ig-frame');
            frame.style.cssText = 'width:420px;height:525px;max-width:none;border-radius:0;box-shadow:none;overflow:hidden;margin:0;';
            const viewport = document.querySelector('.carousel-viewport');
            viewport.style.cssText = 'width:420px;height:525px;aspect-ratio:unset;overflow:hidden;cursor:default;';
            document.body.style.cssText = 'padding:0;margin:0;display:block;overflow:hidden;';
        }""")
        await page.wait_for_timeout(500)

        for i in range(TOTAL_SLIDES):
            await page.evaluate("""(idx) => {
                const track = document.querySelector('.carousel-track');
                track.style.transition = 'none';
                track.style.transform = 'translateX(' + (-idx * 420) + 'px)';
            }""", i)
            await page.wait_for_timeout(400)
            await page.screenshot(
                path=str(OUTPUT_DIR / f"slide-{i+1:02d}.png"),
                clip={"x": 0, "y": 0, "width": VIEW_W, "height": VIEW_H}
            )
            print(f"Exported slide {i+1}/{TOTAL_SLIDES}")

        await browser.close()

asyncio.run(export_slides())
```

**Common mistakes to avoid:**

| Mistake | Result | Fix |
|---|---|---|
| Viewport set to 1080×1350 | Layout reflows, fonts shrink, spacing breaks | Keep viewport 420×525, scale via `device_scale_factor` |
| HTML built with shell scripts | `$`, backticks, numbers get shell-interpolated and corrupt content | Always generate HTML with Python `Path.write_text()` |
| No font-load wait | Headings fall back to system font | `wait_for_timeout(3000)` after `set_content` |
| IG chrome left visible | Header/dots/caption show up in the exported image | Hide `.ig-header,.ig-dots,.ig-actions,.ig-caption` before screenshotting |
| `.ig-frame` width changed | Entire layout shifts vs. preview | Always keep frame at exactly 420px |
| Uploaded image MIME mismatch | Broken/garbled image in render | Check actual format with `file` command, use correct `data:image/...` prefix |

---

## Step 14: Instagram Caption

After the carousel, generate a caption with:

1. Strong opening line
2. Short explanation
3. CTA
4. Brand handle
5. Relevant hashtags

Match the caption's tone to the brand tone selected in Step 1. Keep it concise unless the user requests a long-form caption.

---

## Step 15: Final Deliverables

For every carousel request, provide:

1. Full self-contained HTML carousel
2. Slide-by-slide content summary
3. Instagram caption + hashtags
4. Playwright export script, if requested

If generating files:

```text
carousel.html
export-slides.py
/exports/slide-01.png
/exports/slide-02.png
...
```

---

## Quality Checklist

Before finalizing, confirm:

- [ ] Brand details (name, handle, color, font, tone) are reflected throughout
- [ ] All colors trace back to the one derived palette — no off-system colors
- [ ] Slide size is correct and built at 420×525 (not reflowed at 1080px)
- [ ] Text is readable on mobile at actual export scale
- [ ] Each slide has exactly one clear message
- [ ] Visual hierarchy is strong; heading font and body font roles aren't mixed
- [ ] Layout style varies slide-to-slide while components stay consistent
- [ ] Light/dark backgrounds alternate for rhythm
- [ ] Progress bar is present and accurate on every slide; counter reads correctly
- [ ] Swipe arrow appears on every slide except the last
- [ ] Last slide is structurally distinct: brand gradient, full progress bar, no arrow, CTA button
- [ ] Carousel is swipeable, has next/prev controls, dots, and keyboard navigation
- [ ] Every slide is independently export-ready as a fixed `.slide` container
- [ ] CTA is clear; caption includes the IG handle and hashtags
- [ ] No placeholder text remains; no fake logos or unauthorized brand assets are used
- [ ] Images (if any) are embedded as base64 and cropped/framed cleanly

---

## Design Principles (the "why")

1. Every slide is export-ready as-is — UI elements are part of the image, not overlay.
2. Light/dark alternation sustains attention across the swipe sequence.
3. Heading font = impact, body font = readability — never mix their roles.
4. One primary color drives the entire palette — keeps the carousel cohesive without manual color picking.
5. Progress bar + arrow = progressive disclosure, guiding the swipe forward.
6. The last slide is structurally different (no arrow, full bar) — it has to *feel* like the end.
7. Components repeat identically across slides (same tag style, same row style, same spacing) — consistency reads as intentional design.
8. Content padding always clears the progress bar — nothing overlaps interactive/UI zones.
9. Iterate on individual slides during review; don't rebuild the whole deck for one fix.

---

## Default Behavior

If the user gives complete brand details, generate the carousel immediately. If key brand details are missing, ask for them first. If the user says "you decide," choose a clean, modern, high-contrast design and briefly explain the assumptions before generating.
