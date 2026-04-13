# Refchi Releases

This repository hosts releases for the [Refchi](https://refchi.com) desktop app — a free, local-first creative asset manager for Windows and macOS.

## Download

| Platform | Type | Download |
|----------|------|----------|
| Windows | Installer | [Refchi Setup 0.7.8.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.7.8/Refchi-Setup-0.7.8.exe) |
| Windows | Portable | [Refchi 0.7.8.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.7.8/Refchi-0.7.8.exe) |

Full release history: [refchi.com/landing/releases](https://refchi.com/landing/releases)

---

## Release Notes

### v0.7.8 — April 13, 2026 *(Latest)*
New logo, Agbalumo logotype, accessibility pass, performance improvements

**New**
- New Refchi logo and favicon — custom 'r' mark replaces placeholder icon
- Agbalumo logotype in the title bar and all landing pages
- Dark mode logo variant — title bar icon adapts correctly in dark theme

**Improved**
- macOS title bar: increased left padding so traffic light buttons never overlap the logotype
- Asset card is now a native button — better keyboard navigation and screen reader support
- Sort direction is now field-aware: Name sorts A→Z by default, dates and size sort newest/largest first
- Section headers and empty-state text in sidebar bumped to higher contrast
- Asset card dimensions and tag labels now meet WCAG AA contrast at small sizes
- Status bar filter labels are now fully legible at all sizes
- Faster startup — heavy components now load on demand
- Smoother performance when browsing large libraries
- Smart collection rule editor no longer glitches when removing a rule mid-list

**Fixed**
- Smart collection name field correctly associated with its label for screen readers
- Preview and clipboard dialogs now correctly trap focus for screen readers
- Tag selector now works correctly with keyboard and screen readers
- Navigation and inspector panels now have proper accessibility landmark labels
- Inspector tag dropdown now closes when clicking outside
- Reveal in Explorer no longer silently fails if the path is unavailable

---

### v0.7.7 — April 12, 2026
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
- Various UI consistency improvements across the app

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
- Drag-and-drop reliability improvements

**Fixed**
- Accessibility, performance, and visual consistency improvements
- Drag-and-drop import is faster and more reliable
- Text extraction now works reliably when importing multiple files at once
- Opening an asset's source URL no longer blocks navigation
- Various edge cases in URL handling and panel resizing fixed

**Removed**
- Gaussian blur effect removed from preview
- Preview info bar removed — details now live in the inspector
