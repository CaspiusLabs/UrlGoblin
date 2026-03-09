##UrlGoblin — Feature Summary

**Core Functionality**
•	Automatic clipboard URL capture — monitors the system clipboard and captures any URLs (http, https, ftp, mailto, www) automatically
•	Duplicate detection — prevents the same URL from being added twice across all groups
•	Page title fetching — automatically downloads and displays the <title> from each captured URL
•	Favicon fetching — downloads 16×16 favicons via Google's favicon service and displays them in the list
•	SQLite persistence — all URL data, groups, tags, and associations are stored in a local Db file
•	INI settings persistence — user preferences saved in a .ini file next to the executable

**URL Management**
•	ListView with 5 columns — Title, URL, Tags, Captured (timestamp), Updated (timestamp)
•	Inline title editing — rename URL titles directly in the list (F2 key or menu)
•	Edit URL — change a URL while preserving its tags, timestamps, and group membership (F4)
•	Copy to clipboard — copy selected URL back to clipboard for pasting (F5)
•	Open in browser — launch selected URL in the default browser (F3)
•	Delete selected / Delete all — remove individual or all URLs (F8)
•	Live search — real-time search-as-you-type filtering by title or URL
•	Column sorting — click column headers to sort ascending/descending with arrow indicators
•	Column resizing — user-resized column widths are saved and restored

**Group System**
•	Named groups — organize URLs into collapsible ListView groups (F7 to add)
•	Default "Uncategorized" group — auto-created for clipboard captures
•	Rename / Delete groups — via menu or right-click context menu
•	Move group up/down — reorder groups with persistent sort order
•	Move URL between groups — right-click → "Move URL to Group" submenu
•	Group order persistence — stored in SQLite with sort_order

**Tag System**
•	Global tag registry — create named tags available across all URLs (F6 to add)
•	Multi-tag assignment — assign multiple tags to any URL via a checklist picker dialog
•	Tag pill rendering — colored rounded-rectangle pills drawn in the Tags column via custom draw
•	Tag color hashing — each tag name gets a deterministic color from an 8-color palette
•	Filter by tag — ComboBox dropdown to filter the entire ListView by a single tag
•	Rename / Delete tags — changes propagate to all tagged URLs
•	Tag timestamps — tracks when each tag was last modified

**Menu & Keyboard Shortcuts**
•	Full menu bar — File, URLs, Tags, Groups, Help menus built dynamically in code
•	Accelerator keys — F1 (About), F2 (Edit Title), F3 (Open), F4 (Edit URL), F5 (Copy), F6 (Add Tag), F7 (Add Group), F8 (Delete)
•	Shortcut labels in menus — all accelerator keys displayed as right-aligned text in menu items
•	Right-click context menu — full context menu on ListView items with all URL/group operations
•	Menu item enable/disable — items grayed out contextually (no selection, no groups, etc.)

**System Tray Integration**
•	Tray icon — always present in the notification area
•	Minimize to tray — minimizing or hiding sends the window to tray
•	Restore from tray — double-click tray icon restores window position
•	Tray context menu — Restore, Options, About, Exit
•	Balloon notifications — optional popup when a new URL is captured

**Global Hotkey**
•	Customizable show/hide hotkey — default Ctrl+Shift+G, toggle main window visibility from anywhere
•	Hotkey picker in Options — uses the msctls_hotkey32 control for intuitive key combination selection
•	Persisted in INI — modifier and virtual key saved/loaded across sessions

**Options Dialog**
•	Show notification on new URL — toggle balloon notifications
•	Show on startup — start visible or hidden to tray
•	Always on top — keep window above all others
•	Dark mode — full dark theme toggle
•	Show/Hide hotkey — customizable global hotkey picker
•	Reset window position — restore default centered size

**Dark Mode**
•	Full dark theme — dark title bar, menu bar, ListView, buttons, dialogs, scrollbars
•	Undocumented Windows 10 APIs — SetPreferredAppMode, AllowDarkModeForWindow, FlushMenuThemes via uxtheme ordinals
•	DWM dark title bar — DWMWA_USE_IMMERSIVE_DARK_MODE attribute
•	Owner-drawn buttons — custom dark button painting with press/focus states
•	Dark header custom draw — white text on dark column headers
•	Dark dialog support — Options, Input, Tags Picker, and About dialogs all respect dark mode
•	Themed controls — DarkMode_CFD and DarkMode_ItemsView window themes applied

**Version & Build System**
•	VERSIONINFO resource — 4-part version (MAJOR.MINOR.PATCH.BUILD) embedded in the executable
•	Auto-increment build number — increment_build.ps1 runs as a Pre-Build Event on Release builds, updates Resource.h
•	version.json generation — generate_version_json.ps1 runs as a Post-Build Event, outputs a JSON file with version, download URL, and changelog
•	Single source of truth — all version strings (APP_VERSION, APP_VERSION_W, APP_NAME_VERSION) auto-updated from numeric defines

**Technical Details**
•	Pure Win32/C++20 — no MFC, no .NET, no external UI frameworks
•	In-memory dialog templates — all dialogs (Options, Input, Tags Picker) built programmatically without UrlGoblin.rc resources (except About)
•	GDI+ for favicon PNGs — IStream → Bitmap → hIcon pipeline
•	WinInet for HTTP — favicon and title downloads with 2-second timeouts

•	ComCtl32 v6 manifest — visual styles enabled via linker pragma
