# Refchi Releases

This repository hosts releases for the [Refchi](https://refchi.com) desktop app — a free, local-first creative asset manager for Windows and macOS.

## Download

| Platform | Type | Download |
|----------|------|----------|
| Windows | Installer | [Refchi-Setup-0.8.9.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.8.9/Refchi-Setup-0.8.9.exe) |
| Windows | Portable | [Refchi-0.8.9.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.8.9/Refchi-0.8.9.exe) |

Full release history: [refchi.com/landing/releases](https://refchi.com/landing/releases)

---

## Release Notes

### v0.8.9 — April 14, 2026 *(Latest)*
Preview fixes, embedded URL view, and sidebar rename bug fix

**New**
- URL assets now open in an embedded browser view inside the preview modal — a toolbar shows the URL with options to go back to the card view or open in the system browser

**Fixed**
- SVG files now preview reliably via data URI — bypasses local-file protocol issues on Windows
- Screenshot editor no longer shows a blank canvas when the image fails to load — it now dismisses cleanly
- Inline rename in the sidebar no longer double-saves when pressing Enter — the blur event is now correctly suppressed

---

### v0.8.8 — April 14, 2026
i18n pass, accessibility hardening, reduced-motion support

**Improved**
- Inspector panel is now fully translated — all labels, buttons, and status strings respect the active language
- Added 16 missing locale keys for AI Analysis, OCR controls, and preview actions (English and Turkish)
- Spinners now respect the system's Reduce motion preference and stop animating when it is enabled
- All icon-only buttons in the title bar, inspector, bulk action bar, and sidebar context menu now have proper accessible labels
- Sidebar context menu (Rename / Delete) uses translated strings instead of hardcoded English
- Bulk action bar tag dropdown exposes correct ARIA roles (menu / menuitem) and expanded state
- Electron drag region moved from inline style objects to reusable CSS utility classes

**Fixed**
- mainWindow initialized to null instead of undefined

---

### v0.8.7 — April 14, 2026
OCR and semantic search wired, AI hint banners, preview fixes, leaner exe

**New**
- OCR text extraction is now manually triggerable from the inspector — click 'Extract text' on any image to run on-device OCR via Tesseract.js
- Semantic search is now active — type a phrase in the search bar and AI ranks results by meaning, not just filename
- First-run AI hint banners explain semantic search and OCR once, then dismiss permanently
- SVG files now preview correctly in the preview modal on Windows (MIME type was misreported by the OS)
- TXT files now show a loading spinner while reading, then render the full text content
- Non-Lottie JSON files now display as raw text instead of showing a generic file icon

**Improved**
- Image preview in preview modal no longer overlaps the color palette row — max height capped to 80vh
- Inspector 'Extracted text' section increased to 4 lines of preview
- Exe size reduced ~10–35MB by excluding source maps, TypeScript type declarations, and unused @xenova/transformers source files from the build

---

### v0.8.6 — April 14, 2026
UI quality pass — performance, accessibility, and full i18n coverage

**Improved**
- Notes panel collapse animation now uses width transition instead of grid-template-columns — no more layout thrashing
- All color swatch hover states replaced with ring/opacity feedback — no more hitbox mismatch from CSS transforms
- Bookmark fallback card replaced gradient with neutral background and Globe icon
- Preview modal color chips enlarged and use opacity hover instead of scale-150
- Model thumbnail placeholder now uses flat background instead of gradient
- Toast slide-in animation respects prefers-reduced-motion
- Notes panel collapse animation respects prefers-reduced-motion
- Density +/- buttons now show cursor-not-allowed when disabled

**Fixed**
- Inspector preview images now load lazily — no unnecessary network/disk reads when scrolling
- Status bar refreshing dots use correct fg-tertiary token instead of bg-current
- i18n default context now resolves against bundled English — translation keys never leak as raw strings outside a provider

**New**
- Full i18n coverage: toolbar type/sort labels, status bar, grid toolbar, import modal, toast messages, and inspector all use translation keys
- Turkish translations updated with all new keys

---

### v0.8.5 — April 14, 2026
Turkish i18n, settings panel fixes, dark mode contrast, dropdown flash fix

**New**
- Turkish translation — full UI localization via Settings → General → Interface language
- i18n infrastructure — reusable translation script supports any language via DeepSeek API (`node scripts/translate.js <lang_code> <lang_name>`)
- Export Library (JSON) and Import Library (JSON) buttons in Settings → Advanced are now fully functional
- Clear Thumbnail Cache button in Settings → Advanced now calls the Electron session cache clear

**Fixed**
- Advanced panel toggles (Hardware acceleration, Lazy load thumbnails, Show debug console) now save to preferences instead of being hardcoded
- Dark theme contrast in Appearance panel — unselected theme and tint buttons now use stronger text and background tokens
- Light theme dropdown flash — added `color-scheme: light/dark` CSS to `.light-mode`/`.dark-mode` so native OS controls render in the correct theme without flashing
- Drop zone now imports partial batches gracefully — if one file in a multi-file drop fails to read, the rest still import instead of aborting the whole batch
- Smart Folders section in sidebar now shows the correct label instead of 'S-FOLDERS'

---

### v0.8.4 — April 14, 2026
Text snippets, trash permanent delete, accessibility and performance improvements

**New**
- Save text snippets directly as library assets — use the text button in the sidebar or empty state, paste from clipboard or type, saved under a Text Snippets tag

**Fixed**
- Items already in trash now permanently delete when you choose Delete — previously the trash dialog appeared and did nothing
- Context menu in the trash view now shows "Delete permanently" instead of "Move to trash"
- Preview modal and Clipboard panel now correctly trap keyboard focus — Tab no longer leaks into background content
- Toolbar filter, sort, and color dropdowns now have correct ARIA roles — screen readers no longer see invalid listbox/option on button elements
- Asset filePath field typed as optional — URL assets and text snippets no longer carry a misleading required-but-empty field

**Improved**
- Asset grid re-renders dramatically reduced — selecting one card no longer triggers re-renders for all other cards
- Drop zone now surfaces an error notification if a file import fails instead of silently doing nothing
- Bulk action bar disables all buttons during in-progress operations to prevent double-submits
- Notes save now flashes a brief "Saved" confirmation in the inspector
- Memoized additional components: SidebarItem, FolderTreeItem, NotesView, AssetList, ColumnHeader

---

### v0.8.3 — April 13, 2026
Fix selection ring and card footer color

**Fixed**
- Selection ring now renders correctly on all four sides — restored z-20 absolute ring div; inset box-shadow was being buried under card content
- Card footer is now visibly lighter than the canvas background in both light and dark modes

---

### v0.8.2 — April 13, 2026
UI hardening: selection ring, card height, toggle hitbox, about logo

**Fixed**
- Selection ring no longer clips on the right edge of cards — moved to inset box-shadow which is immune to column layout clipping
- Portrait image thumbnails (PDFs, tall images) capped at 260px height — cards no longer grow excessively tall while images load
- Settings toggle rows now use a single button element — eliminates the misaligned hitbox from the old label+button nesting
- About page now shows the correct app icon instead of the placeholder layers icon

---

### v0.8.1 — April 13, 2026
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
