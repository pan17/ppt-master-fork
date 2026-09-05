---
deck_id: fii_2026_light
kind: deck
category: brand
summary: FII 2026 light corporate reporting and professional briefing presentations for clear narrative delivery and review.
keywords: [FII, corporate, briefing, Traditional Chinese, light]
primary_color: "#000000"
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

# FII 2026 Light — Design Specification

## I. Template Overview

| Application context | Definition |
| --- | --- |
| Recurring presentation family | Corporate reports, technical sharing, business presentations, confidential-business briefings, and patent/application presentations |
| Intended audiences and outcomes | Professional stakeholders and review audiences; support clear understanding of the narrative, evidence, and next steps |
| Delivery and reading assumptions | Primarily presented in meetings, while remaining legible for handoff and close review; page meaning must remain recognizable without speaker narration |
| Representative narrative/page roles | Cover, table of contents, chapter divider, open content page, and closing page |

The template preserves the source's light, premium corporate visual language: full-bleed photographic backgrounds, black primary typography on light content pages, white page-number folios, and white typography on cover and ending pages; the content prototype uses an open content area without any decorative border. The page prototypes form five distinct reusable page families under one FII master identity.

## II. Color Scheme

| Role | Color | Application |
| --- | --- | --- |
| Black | #000000 | Content, chapter, and TOC text |
| White | #FFFFFF | Cover, ending, and page-number text |
| Deep blue | #001F45 | Ending rounded translucent text panel |

## III. Typography

| Role | Font stack | Application |
| --- | --- | --- |
| Chinese headings | `Source Han Sans CN Heavy`, `Microsoft YaHei`, `微软雅黑`, sans-serif | Cover, page, chapter, and TOC headings |
| Chinese body | `Microsoft YaHei`, `微软雅黑`, sans-serif | Subtitles, descriptions, source labels, and supporting text |

The source hierarchy uses a 72px cover title, 44–48px page and chapter headings, 24–28px section labels, 16–22px body copy, and 14–18px metadata.

## IV. Signature Design Elements

- Full-canvas direct picture atoms use `cover_bg.jpg`, `content_bg.jpg`, or `ending_bg.jpg` without a defs/use indirection.
- Cover and ending pages use centered white typography over photographic backgrounds.
- TOC, chapter, and content pages use black typography over the shared content background, with white page-number folios at the lower right and no decorative bars, accent lines, or content-area dashed frames.
- The ending prototype retains the deep-blue `#001F45` rounded translucent overlay behind the closing text.
- All reusable content regions are top-level slot groups with one direct native carrier.
- Page-number folio on TOC, chapter, and content pages is a **locked visual anchor**. Slot bounds `(1125, 699)–(1220, 723)` and carrier anchor `(x=1220, y=714, text-anchor="end")` are fixed by the template. The slot carries `data-pptx-locked="true"` and `data-pptx-locked-anchor="1220 714"`; the carrier carries `data-pptx-locked-carrier="true"`. Downstream authoring must not rewrite these coordinates, reposition the folio toward any background shape (e.g. a coloured panel inside `content_bg.jpg`), or alter slot dimensions. The folio is a non-overridable template fixture.

## V. Page Roster

| File | Master | Layout key | PowerPoint picker name | Visual character | Reusable slots | Structural capacity |
| --- | --- | --- | --- | --- | --- | --- |
| `01_cover.svg` | FII Light Master | cover | Cover | Full-bleed cover photograph with centered white title cluster and lower metadata | title, subtitle, date, body | Four text slots; fixed full-canvas background |
| `02_toc.svg` | FII Light Master | toc | Table of Contents | Light photographic page with black heading and four vertically spaced agenda rows, each with title and description | title, eight body entries (title + description pairs), slide-number | Ten text slots; fixed full-canvas background |
| `03_chapter.svg` | FII Light Master | chapter | Chapter Divider | Light photographic divider with oversized chapter number and left-aligned chapter copy | body, title, subtitle, slide-number | Four text slots; fixed full-canvas background |
| `04_content.svg` | FII Light Master | content | Title and Content | Light photographic content page with black title, open content area, source, and folio | title, object, footer, slide-number | Four slots; fixed full-canvas background |
| `05_ending.svg` | FII Light Master | ending | Closing | Full-bleed ending photograph with deep-blue translucent rounded panel and centered white closing copy | title, subtitle, body, date | Four text slots; fixed background and overlay |

## VI. Assets

| File | Intended usage |
| --- | --- |
| `cover_bg.jpg` | Full-canvas background for `01_cover.svg` |
| `content_bg.jpg` | Full-canvas background for `02_toc.svg`, `03_chapter.svg`, and `04_content.svg` |
| `ending_bg.jpg` | Full-canvas background for `05_ending.svg` |

## VII. Placeholder Overrides

| Placeholder | Override |
| --- | --- |
| TOC entries | Use indexed `{{TOC_ITEM_<N>_TITLE}}` and `{{TOC_ITEM_<N>_DESC}}` pairs (N = 1..4) so generated decks can fill title and description independently |
| `object` | Content page open area uses one direct text carrier labelled `{{CONTENT_AREA}}`; generated content may replace this carrier with one compatible object. |
| `slide-number` (folio) | Locked visual anchor; carrier position, slot bounds, and font are fixed by the template and must not be rewritten. |
