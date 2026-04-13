# Refchi Releases

This repository hosts releases for the [Refchi](https://refchi.com) desktop app — a free, local-first creative asset manager for Windows and macOS.

## Download

| Platform | Type | Download |
|----------|------|----------|
| Windows | Installer | [Refchi-Setup-0.8.1.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.8.1/Refchi-Setup-0.8.1.exe) |
| Windows | Portable | [Refchi-0.8.1.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.8.1/Refchi-0.8.1.exe) |

Full release history: [refchi.com/landing/releases](https://refchi.com/landing/releases)

---

## Release Notes

### v0.8.1 — April 13, 2026 *(Latest)*
Bug fix: asset selection and card height

**Fixed**
- Asset selection restored — clicking any card now correctly selects it and shows the selection ring
- Non-visual asset cards (PDFs, 3D files, documents) no longer grow excessively tall at high grid densities

---

### v0.8.0 — April 13, 2026
Accessibility hardening, bug fixes, and production polish

**Improved**
- All interactive elements are now native buttons — better keyboard navigation and screen reader support across the board
- Bookmark cards converted to native button elements with proper selection state
- Color filter clear button now fully keyboard-accessible
- Theme toggle on the website now announces its state to screen readers
- Inspector color palette: 'Copy all colors' button properly labelled for assistive technology
- Demo UI in landing page correctly marked as decorative for screen readers

**Fixed**
- Update checker no longer accumulates stale timeouts — checking for updates multiple times in a row no longer causes delayed UI glitches
- App version now sourced directly from package.json — version in settings, landing page, and release notes always stay in sync
- Sidebar empty states (no folders, no smart folders, no tags) now render consistently with the shared empty-state component

---

### v0.7.8 — April 13, 2026
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
