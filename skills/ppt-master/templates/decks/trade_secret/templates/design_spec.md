---
deck_id: trade_secret
kind: deck
category: special
summary: 营业秘密模板，用于营业秘密技术说明、机密技术交底、保密审查与专利／软著附件，以纯文字为主，呈现版面稳定、可审计的披露格式。
keywords: [营业秘密, 技术说明, 保密审查]
primary_color: "#000000"
canvas_format: ppt169
canvas_width: 1280
canvas_height: 720
canvas_viewbox: "0 0 1280 720"
source_canvas_width: 1280
source_canvas_height: 720
source_viewbox: "0 0 1280 720"
replication_mode: standard
native_structure_mode: structured
page_count: 3
---

# 营业秘密模板 — 设计规格

## I. 模板概述

| 应用场景 | 定义 |
| --- | --- |
| 反复出现的演示族 | 营业秘密／机密技术说明、专利交底书附件、软著申报附件、保密评审与披露 |
| 目标受众与目的 | 内部技术评审委员、知识产权／法务人员、外部技术专家；传达技术要点并保留可审计的版面结构 |
| 交付与阅读假设 | 现场宣讲与会后单独阅读皆可；以可打印、可归档为前提，单页含义不依赖讲者口述 |
| 典型叙事与页角色 | 封面、技术领域、发明背景、发明特征（以文字为主）、结语；不预设目录页与章节页 |

视觉基调：浅色摄影背景上的纯黑正文、封面与结语用白色字、结语覆盖深蓝半透明面板，形成"稳定、可审计、不喧哗"的版面气氛。

## II. 配色方案

| 角色 | 颜色 | 应用 |
| --- | --- | --- |
| 黑色 | #000000 | 正文、章节、目录、页脚 |
| 白色 | #FFFFFF | 封面、结语文字、页码 |
| 深蓝 | #001F45 | 结语圆角半透明面板底色 |

页码与封面／结语采用白色字，正文与目录采用黑色字，底色由三张全幅 JPG 摄影图统一控制。

## III. 字体（强约束）

| 角色 | 字体堆栈 | 应用 | **字号（必填）** |
| --- | --- | --- | --- |
| 封面主标题 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 封面中央主标题 | **60px** |
| 页标题 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 各正文页页标题 | **36px** |
| 正文 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 正文页内容区正文（基准） | **27px** |
| 说明 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 副标题、说明、提示、关键词 | **18px** |
| 页脚／来源 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 页脚、来源标签、章节标识 | **12px** |
| 页码 | `Microsoft YaHei`, `微软雅黑`, sans-serif | 右下角页码（锁定槽位） | **14px** |

### 强约束规则

1. **字号必填**：上表"字号（必填）"列是硬约束，下游应用不得偏离。允许的唯一例外见下文 §III.1。
2. **正文基准 27px**：正文页 `{{CONTENT_AREA}}` 内容区文字必须以 **27px** 为基准字号；任何子段（如小标题、加粗段）通过 `font-weight="bold"` 或 `tspan` 区分层级，但不得擅自缩小字号。
3. **行内强调允许 `font-size` 微调**：纯装饰性的行内关键词（如「**注意**」「**关键**」前缀）允许在 27px 基础上用 `font-weight="bold"` 加重，**不得**用缩小字号来制造层级。
4. **段间层级只允许粗体**：段标题、副标题、关键词用 `font-weight="bold"` 与正文 27px 区分；如需更突出的层级，仍用 27px + bold，不允许降到 18px / 20px。
5. **来源标签 12px 不可省**：每页必须有 12px 来源标签（footer 槽位），即使来源是"-"占位也不得删除或改字号。
6. **页码 14px 锁定**：右下角页码固定 14px，由 `data-pptx-locked="true"` 锁住位置；下游只能替换 `{{PAGE_NUM}}/{{TOTAL_PAGES}}` 文本。
7. **检查器闸门**：svg_quality_checker 在 §III 字号偏离时将报错（不再只是 advisory），export 在字号偏离模板时拒绝输出。

### §III.1 字号例外（仅限以下场景）

| 场景 | 例外字号 | 备注 |
| --- | --- | --- |
| 页内关键词 / 脚注 | **18px** | 允许 18px 关键词（说明层级），但正文段落不得用 |

正文页（`content` Layout）的 `{{CONTENT_AREA}}` 文字、页标题、页脚、页码**严格禁止**使用 §III.1 例外字号。

### §III.2 自检清单

下游生成 svg_output 时，对每张正文页自查：

- [ ] `content-title-carrier` 是 `font-size="36"`
- [ ] `content-object-carrier` 是 `font-size="27"`（或继承根 `font-size="27"`）
- [ ] 内容区内任何 `<tspan>` 的 `font-size` ∈ {27, bold-27}，不允许 17 / 18 / 20 / 22
- [ ] `content-source-carrier` 是 `font-size="12"`
- [ ] `content-folio-carrier` 是 `font-size="14"` 且 `data-pptx-locked="true"` 不可改
- [ ] 正文页遵守 §III.3：同一段落的中间行撑满可用宽度，禁止提前换行

### §III.3 正文排版（文字页硬约束）

仅适用于 `content` Layout（`02_content_text.svg` 及下游据此生成的文字页）。

| 项目 | 约束 |
| --- | --- |
| 内容区槽位 | `data-pptx-bounds="60 130 1160 540"`，不可改 |
| **正文占位符属性** | `data-pptx-placeholder="body"`（**必须**，不得为 `"object"`）—— 否则 PowerPoint 沿用母版默认 `<a:buChar char="•"/>`，会在每段开头画项目符号，详见 §IV |
| 正文起点 | 所有正文 `<tspan>` 一律 `x="110"`，左缘对齐；不得缩进、不得居中、不得两端分散对齐 |
| 可用宽度 | 左缘 x=110 至槽位右缘 x=1220，约 **1110px**；实际折行按 **1060px** 保守宽度计算，避免贴边溢出 |
| 字号与字宽 | 正文 27px；中文约 **3.7 字 / 100px**，每行目标 **36–39 个汉字**（含标点、数字、英文按实测宽度折算） |
| 折行规则 | 同一段落内，**只有当前行再写一字就会越过可用宽度时才换行**；不得按意群、逗号、编号或句子结束提前折行 |
| 行尾形态 | 段落的中间行必须撑满至接近右缘；**仅段落最后一行允许短行** |
| 编号 | 条款用正文里的 `1.` `2.` `3.` 前缀，不用 PPT 项目符号；编号后的续行仍 `x="110"`，不悬挂缩进 |
| 行距 | 同段续行 `dy="32"`–`dy="40"`；段与段、编号项与项之间可略大（`dy="40"`–`dy="56"`），但不得靠加大行距制造提前换行的假象 |

**禁止事项（硬约束）**

1. **禁止提前换行**：不得在行宽仍有余量时插入新 `<tspan>`。典型反例：一行只写了 20 个汉字就换行，右侧留下大片空白。
2. **禁止短行充数**：除段落末行外，任何一行的视觉右缘不得明显短于内容区右缘。
3. **禁止英文／数字单独占行**：长 token（如 `node-forge`、`X-Content-Type-Options`）过宽放不下时，整段移到下一行，上一行仍须用其他词语填满；不得上一行提前结束、下一行孤零零放一个词。
4. **禁止 `text-anchor="middle"` / `"end"`** 用于正文；正文一律左起。封面与结语的居中白字不在本条范围。
5. **禁止把一段话拆成多张卡片或多个文本框**；整页正文必须落在同一个 `content-object-carrier` 里，用位置 `<tspan>` 折行。

**折行作业顺序**

1. 按 27px、可用宽度 1060px 估算每行容量，先写出将要放入的完整段落。
2. 从左往右累加字形宽度，直到再加一字即溢出，再切到下一 `<tspan x="110" dy="…">`。
3. 用 `text_measure.py calibrate` 或目视检查：中间行右缘应接近 x=1170 一带，不得停在页面中部。
4. 段末短行保留；若整页因此超出 540px 高度，优先压缩段间距（`dy`），不得缩小字号、不得提前换行来“腾地方”。

## IV. 标志性设计元素

- 全幅 JPG 摄影背景：`cover_bg.jpg`、`content_bg.jpg`、`ending_bg.jpg`，分别用于封面、目录／正文、结语三组版式；通过 `data-pptx-layer="layout"` 直接挂载为版式固定元素，不允许被改写为内容图。
- 封面与结语使用白字黑底之外的浅／深底，文字一律居中，结语覆盖一个 `#001F45` 半透明圆角面板（fill-opacity 0.7，rx 60）。
- 正文页统一结构：顶部 36px 页标题 → 中部 1160×540 内容区 → 底部 12px 来源标签 → 右下角 14px 页码。
- 文字页正文左缘对齐、中间行撑满可用宽度，禁止提前换行；详见 §III.3。封面与结语仍居中。
- 页码使用 `{{PAGE_NUM}}/{{TOTAL_PAGES}}` 双字段并锁定槽位 `(1125, 699)–(1220, 723)` 与载体 `(1220, 714)`，模板不可改写；下游应用只能替换页码文本。
- **占位符属性与项目符号（必读）**：母版 `slideMaster1.xml` 的 `bodyStyle` 默认带 `<a:buChar char="•"/>`，每个段落开头会画项目符号。`svg_to_pptx` 转换器只在占位符属性为 `"body"` 或 `"subtitle"` 时调用 `_set_placeholder_no_inherited_bullets` 自动注入 `<a:buNone/>`。故 `02_content_text.svg` 的内容占位符必须设为 `data-pptx-placeholder="body"`，否则每段开头会出现 `•` 圆点。

## V. 页面清单

| 文件 | Master | Layout key | PowerPoint 选项名 | 视觉特征 | 可复用槽位 | 结构容量 |
| --- | --- | --- | --- | --- | --- | --- |
| `01_cover.svg` | Trade Secret Master | cover | Cover | 全幅摄影封面，标题／副标题／日期／作者居中白字 | title, subtitle, date, body | 四个文字槽；全幅背景固定 |
| `02_content_text.svg` | Trade Secret Master | content | Title and Content (Text) | 浅色摄影背景上的黑色页标题与正文；单文本内容区，左缘对齐，中间行撑满，禁止提前换行 | title, object, footer, slide-number | 四个槽；全幅背景固定；正文 27px，折行见 §III.3 |
| `05_ending.svg` | Trade Secret Master | ending | Closing | 全幅摄影结语，深蓝半透明面板，白色感谢词、落款与日期 | title, subtitle, body, date | 四个文字槽；固定背景与面板 |

## VI. 资源

| 文件 | 用途 |
| --- | --- |
| `cover_bg.jpg` | 封面页全幅背景 |
| `content_bg.jpg` | 目录、正文、章节页全幅背景 |
| `ending_bg.jpg` | 结语页全幅背景 |

## VII. 占位符约定

| 槽位 | 占位符 | 用途 |
| --- | --- | --- |
| 封面 title | `{{TITLE}}` | 文档标题（如「一种多功能可靠度设备管理系统」） |
| 封面 subtitle | `{{SUBTITLE}}` | 副标题（如「营业秘密技术说明」） |
| 封面 date | `{{DATE}}` | 日期 |
| 封面 author | `{{AUTHOR}}` | 作者／团队与邮箱 |
| 正文 title | `{{PAGE_TITLE}}` | 章节或页标题（如「發明特徵-1：整體方案概述」） |
| 正文 object | `{{CONTENT_AREA}}` | 正文文字（单一文字内容区） |
| 正文 footer | `{{SOURCE}}` | 来源／章节标识（如「营业秘密技术说明｜發明特徵-1」） |
| 正文 slide-number | `{{PAGE_NUM}}/{{TOTAL_PAGES}}` | 页码（锁定） |
| 结语 title | `{{THANK_YOU}}` | 结语主词（如「本案結語」） |
| 结语 subtitle | `{{CLOSING_MESSAGE}}` | 主题词（如「一种多功能可靠度设备管理系统」） |
| 结语 body | `{{CONTACT_INFO}}` | 团队与邮箱 |
| 结语 date | `{{DATE}}` | 日期 |
