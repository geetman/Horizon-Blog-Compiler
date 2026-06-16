# 📰 Nanometer Horizon — Blog Compiler
### *The all-in-one post authoring tool for the NH Blogger theme*

> [!NOTE]
> This tool runs entirely in your browser — no server, no login, no data leaves your machine. Open `index.html` and go.

---

## Table of Contents

- [Overview](#-overview)
- [Block Types](#-block-types)
- [Media Blocks](#-media-blocks)
- [File Import](#-file-import)
- [Table Editor](#-table-editor)
- [Button Groups](#-button-groups)
- [Toggle Blocks](#-toggle-blocks)
- [Output](#-output)
- [UI & Design](#-ui--design)

---

## 🗺 Overview

The Blog Compiler is a **split-panel, block-based post editor** that lets you compose Nanometer Horizon blog posts visually and export clean, theme-ready HTML — no raw HTML editing required.

```
┌──────────────────────┬──────────────────────┐
│   INPUT / BLOCKS     │   PREVIEW / OUTPUT   │
│                      │                      │
│  Paste text →        │  Live rendered view  │
│  Split into blocks   │  or raw HTML output  │
│  Edit each block     │                      │
│  Reorder / delete    │  Copy to clipboard   │
└──────────────────────┴──────────────────────┘
```

| Feature | Status |
|---|---|
| Block-based editing | ✅ |
| Live preview | ✅ |
| One-click HTML copy | ✅ |
| File import (CSV / Image / GIF / Video) | ✅ |
| Custom px sizing | ✅ |
| No build step or server | ✅ |
| Runs fully offline | ✅ |

---

## 🧱 Block Types

Every post is made up of **blocks** — discrete content units you can add, reorder, and delete individually. The type dropdown on each block lets you switch types at any time without losing your text.

### Text Blocks

| Block | Markdown shortcut | Output tag |
|---|---|---|
| `paragraph` | *(default)* | `<p>` |
| `heading 1` | `# ` prefix | `<h1>` |
| `heading 2` | `## ` prefix | `<h2>` |
| `heading 3` | `### ` prefix | `<h3>` |
| `blockquote` | `> ` prefix | `<blockquote><p>` |
| `code block` | ` ``` ` prefix/suffix | `<pre><code>` |

> [!TIP]
> Paste a whole article into the text area and hit **Split into blocks →**. The compiler auto-detects headings, blockquotes, code blocks, and callouts from the raw text.

---

### Callout Blocks

Six callout flavours, each with its own colour, border, and slight tilt in the preview:

| Block | Trigger prefix | Theme colour |
|---|---|---|
| `note` | `Note:` | 🔵 Blue |
| `info` | `Info:` | 🟢 Green |
| `warning` | `Warning:` | 🟠 Orange |
| `alert` | `Alert:` | 🔴 Red |
| `success` | `Success:` | 🟩 Dark green |
| `tip` | `Tip:` | 🟤 Coffee brown |

All callouts output as `<div class="note">`, `<div class="warning">`, etc. — matching the NH theme stylesheet exactly.

---

### Divider Blocks

Three divider variants with no text content to edit:

- **Divider (line)** — outputs `<hr class="divider" />` — gradient sweep
- **Divider (dots)** — outputs `<hr class="divider-dots" />` — centred dot row  
- **Divider (label)** — outputs `<hr class="divider-label" data-label="…" />` — stamped label badge; has a text field for the label

---

## 🖼 Media Blocks

Media blocks (image and video) share the same three-axis sizing system.

### Image Block

**Fields:**
- **Image source** — paste a URL *or* import a local file (see [File Import](#-file-import))
- **Alt text** — accessibility description
- **Caption** — optional `<figcaption>` text rendered below the image

**Three independent sizing axes:**

#### Width
| Preset | Value |
|---|---|
| Full | `100%` |
| Wide | `80%` |
| Half | `50%` |
| Third | `33%` |
| Small | `220px` fixed |
| **Custom** | type any pixel value |

#### Orientation
| Preset | Behaviour |
|---|---|
| Left | `margin-right: auto` — flush left |
| Center | `margin: 0 auto` — horizontally centred |
| Right | `margin-left: auto` — flush right |
| ⬅ Float Left | `float: left` — text wraps around right |
| Float Right ➡ | `float: right` — text wraps around left |
| **Custom** | type a pixel value for `margin-left` offset |

#### Height
| Preset | Value |
|---|---|
| Auto | natural image height |
| 200px | fixed crop (`object-fit: cover`) |
| 320px | fixed crop |
| 480px | fixed crop |
| **Custom** | type any pixel value |

> [!IMPORTANT]
> All sizing outputs as **inline `style` attributes** — not CSS classes — so images look correct in Blogger without depending on the theme stylesheet loading first.

---

### Video / Embed Block

Identical three-axis sizing system to images. Accepts:

- **Embed URLs** — YouTube (`/embed/…`), Vimeo (`player.vimeo.com/…`), or any iframe-compatible URL → outputs `<iframe>`
- **Local video files** — imported via drag-and-drop or file picker → outputs `<video><source>`

#### Width — same presets as image (`Full / Wide / Half / Third / Small / Custom`)
#### Orientation — same presets as image (`Left / Center / Right / Float Left / Float Right / Custom`)

#### Height
| Preset | Value |
|---|---|
| 220px | short — good for audio players, maps |
| 320px | medium |
| 480px | wide cinematic |
| **Custom** | type any pixel value |

> [!NOTE]
> On mobile viewports (≤ 768px), all percentage widths and floated layouts automatically collapse to full-width stacked display via a media query in the output CSS.

---

## 📎 File Import

Drop files directly onto the **import zone** on the Input tab, or click it to open a file picker. Multiple files can be dropped at once — each becomes its own block.

```
📎 Drop or click to import — CSV (table) · Image · GIF · Video
```

| File type | Accepted formats | Block created | Notes |
|---|---|---|---|
| Spreadsheet | `.csv` | `table` | First row becomes column headers; remaining rows become data. Filename used as table label. |
| Image | `image/*` (JPG, PNG, WebP…) | `image` | Read as base64 data URL. Outputs `<img src="data:…">` — no external hosting needed. |
| Animated GIF | `.gif` | `image` | Same as above — preserved as animated GIF. |
| Video | `video/*` (MP4, WebM…) | `video` | Read as base64. Outputs `<video><source>` with correct MIME type. |

> [!WARNING]
> Large video files will produce very large base64 strings in the HTML output. For long videos, prefer embedding via YouTube/Vimeo URL instead.

---

## 📊 Table Editor

Tables are built with a **live visual grid editor** — no HTML required.

<details>
<summary><strong>What you can do in the table editor</strong></summary>

- Edit any **header cell** directly — bold, labelled inputs across the top row
- Edit any **data cell** directly — inline inputs in every row/column intersection
- **+ row** — appends a new empty row at the bottom
- **+ column** — appends a new empty column on the right, updating headers and all rows simultaneously
- **✕ col** buttons — delete any column (minimum 1 column enforced)
- **✕ row** buttons — delete any row (minimum 1 row enforced)
- **Table label** field — optional badge above the table (outputs as `<span class="table-label">`)

</details>

**Output structure:**

```html
<span class="table-label">// My Table</span>
<div class="table-wrap">
  <table>
    <thead>
      <tr>
        <th>Column 1</th>
        <th>Column 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>value</td>
        <td>value</td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## 🔘 Button Groups

Add a row of styled CTA buttons. Each button is configured independently:

| Field | Options |
|---|---|
| Label | any text |
| URL | any href |
| Variant | `primary` · `secondary` · `ghost` · `danger` |
| Arrow glyph | toggle `→` on/off per button |

- Add as many buttons as needed with **+ add button**
- Remove any button with **✕**
- All buttons in one block share a `<div class="btn-group">` wrapper

**Variant preview colours:**

> 🟠 **Primary** — orange fill  
> 🟣 **Secondary** — purple fill  
> ⬜ **Ghost** — transparent with orange border  
> 🔴 **Danger** — red fill

---

## 🔽 Toggle / Spoiler Blocks

Collapsible content sections. Three variants:

| Variant | Style | Use case |
|---|---|---|
| **Default** | Coffee-brown header | General expandable content |
| **Spoiler** | Red header | Plot spoilers, hidden answers |
| **Code** | Typewriter body font + beige bg | Hidden code solutions |

**Fields:**
- **Summary** — the always-visible clickable header line
- **Body** — the content revealed on expand

Outputs as `<div class="nh-toggle">` (or `.spoiler` / `.code-toggle`) using the JS-powered toggle system that Blogger supports — native `<details>` elements are stripped by Blogger's HTML sanitizer, so these divs are used instead.

---

## 📤 Output

<details>
<summary><strong>How the output pipeline works</strong></summary>

1. Each block runs through `toSnippet(b)` which maps block type → HTML string
2. Snippets are joined with newlines
3. The full string is displayed in the **HTML output** tab as a read-only textarea
4. **Copy HTML** writes it to the clipboard in one click
5. Paste directly into Blogger's HTML editor

</details>

> [!TIP]
> Switch to the **HTML output** tab at any time to inspect what will be copied. The output updates live as you edit blocks.

---

## 🎨 UI & Design

The compiler UI is themed to match the Nanometer Horizon aesthetic — a handwritten-on-parchment look built from three typefaces:

| Role | Font |
|---|---|
| UI / handwriting | [Caveat](https://fonts.google.com/specimen/Caveat) |
| Preview headings / output | [Special Elite](https://fonts.google.com/specimen/Special+Elite) (typewriter) |
| Preview body copy | [Merriweather](https://fonts.google.com/specimen/Merriweather) (serif) |

**Design details:**
- Textured paper background via SVG `feTurbulence` noise filter
- Block cards have a slight alternating tilt (`±0.3deg`) for a physical paper-stack feel
- Virtual tape strip pseudo-element on each block card
- Coffee-ring pseudo-element decorates the right panel
- Offset box-shadows on buttons (press-down animation on `:active`)
- All interactive states use the NH colour palette tokens (`--coffee`, `--wood`, `--ink`, etc.)

---

*Built for the [Nanometer Horizon](https://www.blogger.com) blog. Single HTML file — no dependencies, no build step, no internet required after fonts load.*
