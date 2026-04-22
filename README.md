# NFO / ANS Editor

A browser-based editor and viewer for NFO, ANS and ANSI art files. No install, no server — open `index.html` and go.

## Features

### View & Open
- Drag-and-drop or browse for `.nfo` `.ans` `.diz` `.asc` `.txt` files
- Full CP437 character set rendering with authentic **IBM VGA 8x16** bitmap font
- ANSI escape code parser: colors, bold, cursor movement (`ESC[C`, `ESC[H`, etc.)
- Adjustable column width (80 / 160 / auto)

### New Canvas
`[ NEW ▾ ]` opens a dropdown with three options:
- **Empty** — configure columns and rows
- **From clipboard** — reads the system clipboard and auto-detects column width; falls back to the ANSI code dialog if the clipboard is empty or inaccessible
- **From ANSI code** — paste raw ANSI escape sequences into a textarea (supports `\x1b` and `\033` escape notation)

### Edit
- **Text mode** — type directly onto the canvas with active FG/BG color
- **Draw mode** — click or drag to paint cells with any character + color
  - Right-click to erase (drag to erase multiple cells)
- **Select mode** — drag to select a rectangular region
  - Cut / Copy (`Ctrl+C` also copies plain text to the system clipboard) / Paste
  - Paste from system clipboard (`Ctrl+V`) — supports ASCII art and ANSI art from external apps
  - **Move** — click inside a selection and drag to reposition content
- **Eyedropper** — right-click any cell to pick its FG/BG color; or use `[ PICK ]` for one-shot pick
- **256-color picker** — click the FG or BG color button to open a popup with:
  - 16 system colors
  - 6×6×6 color cube (arranged as 6 distinct planes)
  - 24-step grayscale ramp
- Full CP437 character set via the character picker (`F2`)
- Insert / delete rows
- Zoom in/out
- Undo / Redo (50 steps)

### Image → ANSI
Convert any image to ANSI art directly in the browser:
- Configurable column/row count with optional aspect-ratio lock
- **ASCII-tecken mode** — maps pixel luminance to a character density ramp (` .:-=+*#%@`) with palette color per cell
- **Half-block mode** (`▀`) — double vertical resolution using foreground + background color per cell
- **Full-block mode** (`█`) — one palette color per cell
- **256-color mode** — uses all 256 xterm colors for nearest-color matching (much better accuracy for photos)
- Floyd–Steinberg dithering for better color gradients

### Save & Export
- **`[ SAVE ]`** — saves directly back to the original file (Chrome/Edge only via File System Access API); on other browsers the button is disabled
  - `Ctrl+S` triggers save; if no file handle exists a save-as dialog appears
- **`[ EXPORT ▾ ]`** — always downloads a new file:

| Format | Description |
|--------|-------------|
| `.ANS` | ANSI escape codes + color, standard terminal format; 256-color sequences (`38;5;N`) used automatically when needed |
| `.NFO plain` | Raw CP437 text, no color codes, `\r\n` line endings |
| `.HTML` | Self-contained HTML with inline color styles |

### Tabs & Session
- Multiple files open simultaneously in tabs
- Session auto-saved to `localStorage` — reloading the page restores all tabs and canvas content

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+O` | Open file |
| `Ctrl+N` | New (opens dropdown) |
| `Ctrl+S` | Save directly to file (Chrome/Edge) |
| `Ctrl+Shift+S` | Export HTML |
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Ctrl+C` | Copy selection (+ to system clipboard) |
| `Ctrl+X` | Cut selection |
| `Ctrl+V` | Paste — from app clipboard or system clipboard |
| `Tab` | Toggle Text ↔ Draw mode |
| `F2` | Open character picker |
| `Esc` | Exit edit mode / close dialogs |
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

| Feature | Chrome/Edge | Firefox | Safari |
|---------|-------------|---------|--------|
| Editor (view, edit, export) | ✓ | ✓ | ✓ |
| Save directly to file (`Ctrl+S`) | ✓ | — | — |
| Open with file handle | ✓ | — | — |

Direct save requires the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API), supported in Chrome 86+ and Edge 86+.
