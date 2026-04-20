# NFO / ANS Editor

A browser-based editor and viewer for NFO, ANS and ANSI art files. No install, no server — open `index.html` and go.

## Features

### View & Open
- Drag-and-drop or browse for `.nfo` `.ans` `.diz` `.asc` `.txt` files
- Full CP437 character set rendering with authentic **IBM VGA 8x16** bitmap font
- ANSI escape code parser: colors, bold, cursor movement (`ESC[C`, `ESC[H`, etc.)
- Adjustable column width (80 / 160 / auto)

### Edit
- **Text mode** — type directly onto the canvas with active FG/BG color
- **Draw mode** — click or drag to paint cells with any character + color
  - Right-click to erase (drag to erase multiple cells)
- **Select mode** — drag to select a rectangular region
  - Cut / Copy / Paste
  - **Move** — click inside a selection and drag to reposition content
- **Eyedropper** — right-click any cell to pick its FG/BG color; or use `[ PICK ]` for one-shot pick
- 16-color CGA palette for both foreground and background
- Full-block, half-block and any CP437 character via the character picker (`F2`)
- Insert / delete rows
- Zoom in/out
- Undo / Redo (50 steps)

### Image → ANSI
Convert any image to ANSI art directly in the browser:
- Configurable column/row count with optional aspect-ratio lock
- Half-block mode (`▀`) for double vertical resolution
- Floyd–Steinberg dithering for better color gradients

### Export
Single `[ EXPORT ▾ ]` button with three formats:
| Format | Description |
|--------|-------------|
| `.ANS` | ANSI escape codes + color, standard terminal format |
| `.NFO plain` | Raw CP437 text, no color codes, `\r\n` line endings |
| `.HTML` | Self-contained HTML with inline color styles |

### Tabs & Session
- Multiple files open simultaneously in tabs
- Session auto-saved to `localStorage` — reloading the page restores all tabs and canvas content

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+O` | Open file |
| `Ctrl+N` | New canvas |
| `Ctrl+S` | Export ANS |
| `Ctrl+Shift+S` | Export HTML |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Tab` | Toggle Text ↔ Draw mode |
| `F2` | Open character picker |
| `Esc` | Exit edit mode / deselect |
| `Ctrl+Delete` | Delete current row |
| `Ctrl+Insert` | Insert empty row |
| `Ctrl++` / `Ctrl+-` | Zoom in / out |

## Usage

1. Clone or download the repo
2. Place `ibm_vga_8x16.woff` in the same folder (IBM VGA 8x16 font file)
3. Open `index.html` in a modern browser
4. Drop an NFO/ANS file onto the page or click `[ OPEN ]`

No build step, no dependencies, no network required after initial font load.

## Font

The editor uses the **IBM VGA 8x16** bitmap font for authentic rendering. The font file (`ibm_vga_8x16.woff`) is not included in this repo — source it from [int10h.org](https://int10h.org/oldschool-pc-fonts/) (The Ultimate Oldschool PC Font Pack).

## Browser Support

Any modern browser with Canvas 2D, `localStorage`, and `FileReader` API support (Chrome, Firefox, Edge, Safari).
