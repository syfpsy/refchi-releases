# Refchi Releases

This repository hosts releases for the [Refchi](https://refchi.com) desktop app — a free, local-first creative asset manager for Windows and macOS.

## Download

| Platform | Type | Download |
|----------|------|----------|
| Windows | Installer | [Refchi Setup 0.7.7.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.7.7/Refchi-Setup-0.7.7.exe) |
| Windows | Portable | [Refchi 0.7.7.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.7.7/Refchi-0.7.7.exe) |

Full release history: [refchi.com/landing/releases](https://refchi.com/landing/releases)

---

## Release Notes

### v0.7.7 — April 12, 2026 *(Latest)*
System tray: minimize to tray, launch at startup, tray menu

**New**
- Minimize to system tray — app stays in tray when window is closed
- Tray right-click menu: Open, Check for Updates, Launch at Startup, Quit
- Launch at Startup toggle directly from tray menu

---

### v0.7.6 — April 12, 2026
macOS support, new app icon, sidebar polish

**New**
- macOS build — unsigned beta for testing, signed release coming soon
- New app icon — dark monogram on white rounded square

**Improved**
- Sidebar: Smart Folders now appears above Tags
- Default library starts with one folder and a clean set of starter tags
- macOS title bar: traffic lights properly positioned, custom controls hidden

---

### v0.7.5 — April 12, 2026
Canvas mode, notes with calendar, and AI semantic search

**New**
- Canvas editor — freeform board for spatially arranging assets
- Notes with rich text editing (headings, lists, tasks, code blocks, links)
- Note calendar view — browse notes by creation date
- Note bubble menu bar for inline text formatting
- Semantic search — find assets by meaning, not just filename

**Improved**
- Inspector panel sections are now collapsible
- Screenshot editor rewritten — cleaner toolbar and tool layout
- Various UI consistency improvements across app shell

---

### v0.4.0 — April 9, 2026
Cross-platform builds, AI tagging, bookmarks, and design overhaul

**New**
- Cross-platform builds — Windows installer + portable, macOS, and Linux packages
- Auto-updates — app checks for and installs new versions automatically
- Color palette extraction from images with palette filter in grid toolbar
- Smart collections with rule-based filters (type, tag, date, color)
- Rich bookmark cards — OG image, favicon, title, description, domain pill
- Video, audio, and GIF native preview support
- AI auto-tagging — on-device classification with confidence scores
- OCR text extraction from images and screenshots on import
- Browser image drag-and-drop — drag directly from web pages
- Clipboard link save — save URLs directly from clipboard panel

**Improved**
- Design overhaul — masonry grid, compact cards, clean chrome
- Light mode polish — all surfaces, bookmarks, inspector, and animations
- AI tags now shown directly on asset cards
- Bookmark metadata fetching with better fallbacks
- Inspector now compact with file-type icons per asset
- Drag-and-drop reliability improvements — multiple import strategies

**Fixed**
- 33 accessibility, performance, and theming audit issues resolved
- Drag-drop import now completes in a single step (no two-pass)
- OCR race condition on concurrent import resolved
- Navigation block when opening asset source URL fixed
- URL download handler and inspector resize edge cases fixed

**Removed**
- Mock/placeholder tags replaced with real AI-generated tags
- Gaussian blur effect removed from preview
- Preview info bar removed (info lives in inspector)

---

### v0.3.0 — April 9, 2026
Lottie thumbnails, screenshot capture, 3D preview, and AI pipeline

**New**
- Lottie animation thumbnails — animated previews in the grid
- Screenshot capture with live area selection on desktop
- Native crop tool for screenshots
- 3D model thumbnails and full interactive preview
- AI classification + OCR pipeline (beta) — fully on-device, no API key needed
- Pin-to-top (always-on-top) window mode
- Title bar logotype and favorites count badge
- Comprehensive settings panel

**Improved**
- Sidebar cleanup — cleaner section structure and nav items
- Inspector panel made compact with file type icons

**Fixed**
- GLB preview rendering issues resolved
- Screenshot live area selection now captures correct desktop region
- Dark mode rendering fix for frameless window

---

### v0.2.2 — April 9, 2026
Drag-drop import fix and screenshot area selection

**Fixed**
- Drag-drop import now reliably saves files to library

**New**
- Screenshot area selection before capture

---

### v0.2.1 — April 9, 2026
Stability fixes for slider, Lottie, drag-drop, blur, and resize

**Fixed**
- Density slider value sync fixed
- Lottie preview stability improvements
- Drag-drop edge cases resolved
- Background blur performance fix
- Panel resize handle stability
- Window reload behavior corrected

---

### v0.2.0 — April 9, 2026
Clipboard manager, screenshot annotation, and multi-select

**New**
- Clipboard manager — monitors and browses clipboard history
- Screenshot capture with annotation editor (draw, crop, annotate)
- Multi-select with bulk operations (tag, move, delete, export)
- URL import — bookmark any web link with metadata fetch
- Resizable panels with drag handles
- Toast notifications and persistent status bar
- File explorer integration (Reveal in Explorer / Finder)
- Collapsible sidebar sections
- Grid keyboard navigation (arrow keys, Enter, Escape)
- Confirm-delete dialog to prevent accidental deletion

**Improved**
- Broad file type support: Lottie, Markdown, PDF, Video, Audio, Font, Archive
- List view with sortable columns
- Folder and tag asset counts in sidebar

**Fixed**
- 20 bugs resolved from thorough audit
