# Refchi Releases

This repository hosts releases for the [Refchi](https://refchi.com) desktop app — a free, local-first creative asset manager for Windows and macOS.

## Download

| Platform | Type | Download |
|----------|------|----------|
| Windows | Installer | [Refchi-Setup-0.9.5.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.9.5/Refchi-Setup-0.9.5.exe) |
| Windows | Portable | [Refchi-0.9.5.exe](https://github.com/syfpsy/refchi-releases/releases/download/v0.9.5/Refchi-0.9.5.exe) |

Full release history: [refchi.com/landing/releases](https://refchi.com/landing/releases)

---

## Release Notes

### v0.9.5 — April 17, 2026 *(Latest)*
CLIP content tagging, fixed sidebar, sidebar toggle

**New**
- Images are now tagged by their actual content using CLIP zero-shot classification — searches like "person", "man", "landscape", "dog", "food" now find matching images even when the filename has no such word. Previously the classifier was pure geometry (aspect ratio, colors, edges) and could only match "photo", "portrait", "landscape" (the orientation).
- ~55 content labels across people, places, animals, objects, design & digital, art & illustration, text — tags appear as asset.contentTags and feed into the semantic search corpus automatically
- Sidebar gained a collapse/expand toggle button on its right edge — click the chevron to slide the sidebar in or out. Preference persists across app restarts.

**Improved**
- Sidebar is now fixed at 224 px wide — no longer user-resizable. The app's typography and spacing is tuned for this width; drag-resize meant labels would overflow or space would be wasted depending on where you stopped.
- Turkish "Import" button now reads "Ekle" instead of the overly-literal "İçe Aktar"

**Fixed**
- CLIP model (~90 MB, Xenova/clip-vit-base-patch32) downloads once on first run and is cached under userData/models. Subsequent runs are instant. Content tagging runs in the background after all other startup tasks so the app stays responsive.

---

### v0.9.4 — April 17, 2026
Semantic search confidence gate

**Improved**
- Semantic search is now gated by both an absolute score floor (0.22, up from 0.12) and a relative filter that requires each result to score at least 70% of the top match — so when the model finds something obviously strong you get that match plus close neighbors, and when it finds nothing confident you fall through to text search instead of seeing a long tail of weakly-related items
- Weak queries that would previously surface 30+ loosely-similar results now correctly fall back to text search, because their top score is already below the absolute floor

---

### v0.9.3 — April 17, 2026
Balanced semantic search, color palette backfill, centered preview palette, clear-search button

**Improved**
- Semantic search threshold tuned to 0.12 — the middle ground between v0.9.2's 0.08 (too loose, noisy long tail) and v0.9.0's 0.15 (too strict, missed filename-only matches)
- Preview modal's color palette is now centered under the image, not right-aligned — visually anchored to the preview
- Preview modal's title, dimensions, size, and asset counter render white with a drop-shadow over the blurred backdrop, instead of muted tokens that disappeared against the glass
- Search bar gained a clear (×) button that appears as soon as you type — the searching/semantic pill tucks to its left so both stay visible during search

**Fixed**
- Images drag-and-dropped from the web now get color palettes — nativeImage occasionally returned empty on just-written files (kernel write-buffer race on Windows); added a readFileSync → createFromBuffer fallback that rescues those cases
- Added a color-palette backfill pass on startup that re-extracts palettes for any image asset with empty colors, catches historical imports and web-drop edge cases the initial extraction missed

---

### v0.9.2 — April 17, 2026
Semantic search + OCR + screenshot editor unblocked

**Fixed**
- Screenshot editor's header buttons, color swatches, and tool buttons (blur, draw, arrow, rect, text) were unclickable on Windows — the frameless title bar's `-webkit-app-region: drag` was bleeding through the editor overlay, so clicks went to the OS window-drag instead of the buttons. Added `app-no-drag-region` to the editor root
- Semantic search silently showed an empty grid when the model returned zero matches above threshold — now falls back to text search so users always see something relevant
- OCR now works offline on first run — bundled English language data (2.9 MB) as extra resources and set Tesseract's `langPath` to the local copy. Previously first-run OCR silently fetched from cdn.jsdelivr.net and failed on any firewall / offline network
- OCR button now appears for all image extensions Tesseract can decode (jpg/jpeg/png/bmp/tiff/webp/gif/pbm/pgm/ppm/pnm), not just assets whose library type happens to be "image" or "gif"

**Improved**
- Semantic search now triggers on any 3+ character query instead of requiring 2 words — single-word queries like "logo" or "minimalist" now go through the model
- Semantic score threshold lowered from 0.15 to 0.08 so legitimate matches from short-corpus assets still rank
- Search bar now shows a "Searching…" spinner pill while the model loads or embeddings are in flight — first-run model download (~22 MB from Hugging Face) no longer looks like the app is hanging
- Renderer now subscribes to AI engine status changes from the main process and surfaces load failures as toasts — if the semantic model or OCR engine fails to initialize, you see it immediately instead of silently getting empty results

---

### v0.9.1 — April 16, 2026
Hotfix: startup crash (missing transitive deps) and bulletproof packaging

**Fixed**
- Startup crash "Cannot find module regenerator-runtime/runtime" — tesseract.js's hoisted transitive deps were trapped inside app.asar while tesseract.js itself lived in app.asar.unpacked, so Node's require walk couldn't find them
- Generated the full transitive dependency closure of tesseract.js and @xenova/transformers and unpacked all 43 runtime deps (regenerator-runtime, node-fetch, bmp-js, @huggingface/jinja, color, semver, streamx, tar-fs, and more) so any require from the unpacked AI packages now resolves

---

### v0.9.0 — April 16, 2026
Stability & cleanup: file logger, diagnostics panel, structured IPC errors, shared utilities

**New**
- Persistent log file at `userData/logs/refchi.log` — every update check, AI engine status change, and unexpected error is recorded with timestamps; auto-rotates at 1 MB
- About panel now shows the library path and log file path with Reveal / Open buttons so support questions take one click instead of a scavenger hunt
- About panel footer shows platform, architecture, Electron and Node versions for bug reports

**Improved**
- Auto-updater now writes every step to the log file — download progress, available versions, errors — so "update didn't work" can be diagnosed after the fact
- Auto-updater fallback timer now flips to a clear "No response from update server" error instead of silently claiming you're up to date when the server is unreachable
- Auto-updater UI cancels its 12-second fallback as soon as a real status event arrives, so late responses can't flip a downloaded-and-ready state back to an error
- Saving library changes now surfaces the real reason if the disk is full or permissions are denied
- Dropping an image URL that fails to download now tells you why (404, non-image content type, network blocked) instead of silently doing nothing
- URL metadata fetcher now returns a fetchFailed flag + reason when bookmark enrichment fails so the UI can distinguish "site has no metadata" from "fetch blocked"
- Embedding cache is now flushed on before-quit as well as window-all-closed, so forced OS shutdowns don't lose search history

**Fixed**
- Consolidated four inline copies of the local-file:// URL decoder (preview modal, image fallback, SVG fallback, text fallback) into a single shared helper — previously a bug fix in one site diverged from the others
- Consolidated three duplicate copies of VISUAL_TYPES / IMAGE_MIME_BY_EXT / MARKDOWN_EXTENSIONS — new file types now only need to be added in one place

---

### v0.8.14 — April 16, 2026
Semantic search + OCR fixed in packaged builds, font preview, code file preview, robust error handling

**Fixed**
- Semantic search now actually works in packaged builds — the installer was excluding the @xenova/transformers ESM entrypoint so the model never loaded; exclusion rules corrected
- OCR now works in packaged builds — tesseract.js is unpacked from the asar archive, worker and core paths are set explicitly so the engine loads on first run
- AI engines now surface real errors instead of failing silently — users see "Semantic search unavailable — using text search" toasts and specific OCR reasons ("No text found", "OCR engine unavailable", etc.)
- Link-mode assets whose source file was moved or deleted now show a clear "File is missing" message in the preview modal instead of a blank area
- Video and audio files that the built-in Chromium player can't decode now show an "Open in default app" fallback instead of a broken player

**New**
- Font files (.ttf, .otf, .woff, .woff2) now preview with a full glyph sample — "Ag" at 72pt, the pangram at 40pt, full character set, and sample paragraphs — all rendered in the actual font via the FontFace API
- Source code and config files preview as syntax-friendly text — .ts, .tsx, .js, .py, .rs, .go, .sh, .sql, .html, .css, .env, .dockerfile, and 30+ more extensions now show their contents inline instead of a generic icon
- Archive files (.zip, .rar, .7z, etc.) show a clear "Reveal in explorer" action so users can extract with their native tool of choice
- Text snippet assets (clipboard-imported text) now preview their stored content directly in the modal

**Improved**
- Semantic search results are now persisted across sessions — embeddings are cached to disk keyed by content hash, so subsequent searches return instantly instead of re-embedding the whole library on every launch
- Lowered semantic search score threshold from 0.25 to 0.15 so filename-only matches still rank
- File reads through IPC are now guarded with a 25 MB cap — a 500 MB log file or oversized SVG no longer freezes the window; oversized text files show a truncated preview with a clear notice
- OCR backfill aborts early if the engine itself fails to load, preventing 100 consecutive failed reads

---

### v0.8.13 — April 16, 2026
OBJ model preview, image preview resilience, media load fallbacks

**New**
- Wavefront .obj 3D models now preview with a full Three.js viewer — orbit controls, auto-centering, and a default material for untextured meshes
- .obj grid thumbnails render a live auto-rotating 3D preview instead of a generic 3D badge

**Fixed**
- Images that fail to load through the local-file:// protocol now fall back to an IPC blob URL — rescues PNG/JPG/WebP files that the custom protocol couldn't stream due to path encoding or MIME edge cases
- Failed image previews now show a clear "Could not load image" message instead of a blank area

---

### v0.8.12 — April 14, 2026
Protocol hardening and dead-code cleanup

**Fixed**
- Local file protocol handler now strips query strings and fragments before decoding paths — prevents edge-case 404s on URLs with unexpected suffixes

**Improved**
- Removed unreachable GIF branch in preview modal — GIF files are already handled by the image renderer

---

### v0.8.11 — April 14, 2026
SVG preview: inline rendering for full fidelity across all SVG types

**Fixed**
- SVG files now render inline in the preview modal instead of as data URIs — eliminates blank previews caused by btoa encoding edge cases and works reliably for all SVG content including complex filters and gradients
- SVG preview now works even when filePath is not set — falls back to deriving the path from previewUrl

---

### v0.8.10 — April 14, 2026
Hotfix: restore image, PDF, audio, and video preview

**Fixed**
- Images, PDFs, audio, and video files no longer show a blank preview — the local-file:// protocol handler was broken by a scheme registration flag added in 0.8.9 that mangled Windows paths during URL normalization

---

### v0.8.9 — April 14, 2026
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
