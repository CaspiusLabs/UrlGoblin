UrlGoblin — Feature Summary.

Technical Details
•	Pure Win32/C++20 — no MFC, no .NET, no external UI frameworks
•	In-memory dialog templates — all dialogs (Options, Input, Tags Picker) built programmatically without UrlGoblin.rc resources (except About)
•	GDI+ for favicon PNGs — IStream → Bitmap → hIcon pipeline
•	WinInet for HTTP — favicon and title downloads with 2-second timeouts
•	ComCtl32 v6 manifest — visual styles enabled via linker pragma

Version & Build System
•	VERSIONINFO resource — 4-part version (MAJOR.MINOR.PATCH.BUILD) embedded in the executable
•	Auto-increment build number — increment_build.ps1 runs as a Pre-Build Event on Release builds, updates Resource.h
•	version.json generation — generate_version_json.ps1 runs as a Post-Build Event, outputs a JSON file with version, download URL, and changelog
•	Single source of truth — all version strings (APP_VERSION, APP_VERSION_W, APP_NAME_VERSION) auto-updated from numeric defines



UrlGoblin — Changelog.

From 1.2.0 - Check for Updates:
•	Added Check for Updates on Startup option.
•	Added manual Check for Updates option.
•	Update Dialog actions dynamically driven by the server response.
•	Added <strong>Download Setup</strong>, <strong>Download Portable</strong>, and <strong>View Changelog</strong> buttons.
•	Added <strong>Skip</strong> button to dismiss update.

From 1.1.9 - Options Dialog:
•	Show notification on new URL — toggle balloon notifications.
•	Show on startup — start visible or hidden to tray.
•	Always on top — keep window above all others.
•	Dark mode — full dark theme toggle.
•	Show/Hide hotkey — customizable global hotkey picker.
•	Reset window position — restore default centered size.

From 1.1.8 - Dark Mode:
•	Full dark theme — dark title bar, menu bar, ListView, buttons, dialogs, scrollbars.
•	Undocumented Windows 10 APIs — SetPreferredAppMode, AllowDarkModeForWindow, FlushMenuThemes via uxtheme ordinals.
•	Owner-drawn buttons — custom dark button painting with press/focus states.
•	Dark header custom draw — white text on dark column headers.
•	Dark dialog support — Options, Input, Tags Picker, and About dialogs all respect dark mode.

From 1.1.7 - Global Hotkey:
•	Customizable show/hide hotkey — default Ctrl+Shift+G, toggle main window visibility from anywhere.
•	Hotkey picker in Options — uses the msctls_hotkey32 control for intuitive key combination selection.
•	Persisted in INI — modifier and virtual key saved/loaded across sessions.

From 1.1.6 - Menu & Keyboard Shortcuts:
•	Full menu bar — File, URLs, Tags, Groups, Help menus built dynamically in code.
•	Accelerator keys — F1 (About), F2 (Edit Title), F3 (Open), F4 (Edit URL), F5 (Copy), F6 (Add Tag), F7 (Add Group), F8 (Delete).
•	Shortcut labels in menus — all accelerator keys displayed as right-aligned text in menu items.
•	Right-click context menu — full context menu on ListView items with all URL/group operations.
•	Menu item enable/disable — items grayed out contextually (no selection, no groups, etc.).

From 1.1.5 - Tag System:
•	Global tag registry — create named tags available across all URLs.
•	Multi-tag assignment — assign multiple tags to any URL via a checklist picker dialog.
•	Tag pill rendering — colored rounded-rectangle pills drawn in the Tags column via custom draw.
•	Tag color hashing — each tag name gets a deterministic color from an 8-color palette.
•	Filter by tag — ComboBox dropdown to filter the entire url list by a single tag.
•	Rename / Delete tags — changes propagate to all tagged URLs.

From 1.1.4 - Group System:
•	Named groups — organize URLs into collapsible groups.
•	Default "Uncategorized" group — auto-created for clipboard captures.
•	Rename / Delete groups — via menu or right-click context menu.
•	Move group up/down — reorder groups with persistent sort order.
•	Move URL between groups — right-click "Move URL to Group" submenu.
•	Group order persistence — stored in SQLite with sort order.

From 1.1.3 - URL Management:
•	Inline title editing — rename URL titles directly in the list.
•	URLs editing from right click menu.
•	Copy to clipboard — copy selected URL back to clipboard for pasting.
•	Open in browser — launch selected URL in the default browser.
•	Delete selected / Delete all — remove individual or all URLs.
•	Column sorting — click column headers to sort ascending/descending with arrow indicators.
•	Column resizing — user-resized column widths are saved and restored.

From 1.1.2 - System Tray Integration:
•	Tray icon — always present in the notification area.
•	Minimize to tray — minimizing or hiding sends the window to tray.
•	Restore from tray — double-click tray icon restores window position.
•	Tray popup when a new URL is captured.

From 1.1.1 - Core Functionality:
•	Automatic clipboard URL capture — monitors the system clipboard and captures any URLs.
•	Duplicate detection — prevents the same URL from being added twice.
•	Page title fetching — automatically downloads and displays title from each captured URL.
•	Favicon fetching — downloads 16×16 favicons via Google favicon service and displays them in the list.
•	SQLite persistence — all data are stored in a local Db file.
•	Settings preferences saved in a INI file.
