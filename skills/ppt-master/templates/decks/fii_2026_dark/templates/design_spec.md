---
deck_id: fii_2026_dark
kind: deck
category: brand
summary: FII 2026 dark corporate reporting and professional briefing presentations for high-contrast narrative delivery in low-light venues and review.
keywords: [FII, corporate, briefing, Traditional Chinese, dark]
primary_color: "#FFFFFF"
canvas_format: ppt169
canvas_width: 1280
canvas_height: 720
canvas_viewbox: "0 0 1280 720"
source_canvas_width: 1280
source_canvas_height: 720
source_viewbox: "0 0 1280 720"
replication_mode: fidelity
native_structure_mode: structured
page_count: 5
---

# FII 2026 Dark — Design Specification

## I. Template Overview

| Application context | Definition |
| --- | --- |
| Recurring presentation family | Corporate reports, technical sharing, business presentations, confidential-business briefings, and patent/application presentations |
| Intended audiences and outcomes | Professional stakeholders and review audiences; support clear understanding of the narrative, evidence, and next steps through high-contrast delivery |
| Delivery and reading assumptions | Primarily presented in meetings and low-light venues, while remaining legible for handoff and close review; page meaning must remain recognizable without speaker narration |
| Representative narrative/page roles | Cover, table of contents, chapter divider, open content page, and closing page |

The template preserves the source's dark, premium corporate visual language: full-bleed blue technology imagery, white typography, restrained spacing, and no decorative lines or content-frame overlays. The five prototypes share one FII dark master identity while exposing distinct reusable Layout contracts.

## II. Color Scheme

| Role | Color | Application |
| --- | --- | --- |
| White | #FFFFFF | All authored text and placeholder carriers |
| Dark blue imagery | Bundled source photography | Full-canvas cover, content, chapter, TOC, and ending backgrounds |

## III. Typography

| Role | Font stack | Application |
| --- | --- | --- |
| Chinese headings | `Source Han Sans CN Heavy`, `Microsoft YaHei`, `微软雅黑`, sans-serif | Cover, page, chapter, and TOC headings |
| Chinese body | `Microsoft YaHei`, `微软雅黑`, sans-serif | Subtitles, descriptions, source labels, and supporting text |

The source hierarchy uses a 72px cover title, 36–48px page and chapter headings, a 120px chapter number, 16–24px body copy, and 12–18px metadata.

## IV. Signature Design Elements

- Full-canvas direct picture atoms use `cover_bg.jpg`, `content_bg.jpg`, or `ending_bg.jpg` without defs/use indirection or an overlay.
- White typography remains the only authored foreground color, preserving high contrast over the source's dark blue photographic backgrounds.
- Cover and ending pages use centered title clusters; chapter, TOC, and content pages use a left-aligned information hierarchy.
- TOC, chapter, and content pages contain no decorative bars, accent lines, or content-area border frames.
- Every reusable content region is a top-level slot group with one direct native carrier.
- Page-number folio on TOC, chapter, and content pages is a **locked visual anchor**. Slot bounds `(1135, 689)–(1230, 713)` and carrier anchor `(x=1230, y=714, text-anchor="end")` are fixed by the template. The slot carries `data-pptx-locked="true"` and `data-pptx-locked-anchor="1230 714"`; the carrier carries `data-pptx-locked-carrier="true"`. Downstream authoring must not rewrite these coordinates, reposition the folio toward any background shape (e.g. a coloured panel inside `content_bg.jpg`), or alter slot dimensions. The folio is a non-overridable template fixture.

## V. Page Roster

| File | Master | Layout key | PowerPoint picker name | Visual character | Reusable slots | Structural capacity |
| --- | --- | --- | --- | --- | --- | --- |
| `01_cover.svg` | FII Dark Master | cover | Cover | Full-bleed dark technology photograph with centered white title cluster and lower metadata | title, subtitle, date, body | Four text slots; fixed full-canvas background |
| `02_toc.svg` | FII Dark Master | toc | Table of Contents | Dark blue technology background with a left-aligned heading and four vertically spaced agenda rows | title, eight agenda text fields, slide-number | Ten text slots; fixed full-canvas background |
| `03_chapter.svg` | FII Dark Master | chapter | Chapter Divider | Dark photographic divider with oversized chapter number and left-aligned chapter copy | body, title, subtitle, slide-number | Four text slots; fixed full-canvas background |
| `04_content.svg` | FII Dark Master | content | Title and Content | Dark photographic content page with white title, borderless open content area, source, and folio | title, object, footer, slide-number | Four slots; fixed full-canvas background |
| `05_ending.svg` | FII Dark Master | ending | Closing | Full-bleed dark technology photograph with centered white closing copy | title, subtitle, body, date | Four text slots; fixed full-canvas background |

## VI. Assets

| File | Intended usage |
| --- | --- |
| `cover_bg.jpg` | Full-canvas background for `01_cover.svg` |
| `content_bg.jpg` | Full-canvas background for `02_toc.svg`, `03_chapter.svg`, and `04_content.svg` |
| `ending_bg.jpg` | Full-canvas background for `05_ending.svg` |

## VII. Placeholder Overrides

| Placeholder | Override |
| --- | --- |
| `object` | The content page open area uses one direct text carrier labelled `{{CONTENT_AREA}}`; generated content may replace this carrier with one compatible object. |
| `slide-number` (folio) | Locked visual anchor; carrier position, slot bounds, and font are fixed by the template and must not be rewritten. |
