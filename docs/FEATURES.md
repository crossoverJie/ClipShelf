# Feature Tracker

> Each feature has a unique ID (`F-XXX`) for tracking. Update the status column as features are implemented.
>
> Status: **Done** | **Partial** | **TODO**

---

## Completed

### Core (Plan Steps 1–6)

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-001 | Menu Bar App | Runs as a menu bar icon with no Dock presence (`LSUIElement`, `NSApplication.setActivationPolicy(.accessory)`) | Done |
| F-002 | Floating Panel | Always-on-top `NSPanel` with vibrancy, visible across all Spaces, draggable by background | Done |
| F-003 | Panel Toggle | Click menu bar icon or press global hotkey to show/hide the panel | Done |
| F-004 | Global Hotkey | ⌘⇧V toggles the panel from any application (Carbon `RegisterEventHotKey`) | Done |
| F-005 | SwiftData Model | `ShelfItem` persists text, images, and files with `@Model`; images use `@Attribute(.externalStorage)` | Done |
| F-006 | Clipboard Paste | ⌘V in the panel reads `NSPasteboard.general` (file > image > text priority) and creates a card | Done |
| F-007 | Clipboard Auto-Monitor | Background polling (0.5s) detects clipboard changes, skips self-writes, auto-captures content | Done |
| F-008 | One-click Copy | Click any card to copy its content back to the system clipboard | Done |
| F-009 | Drag & Drop In | Drop text, images, or files onto the panel via `onDrop` with multiple UTTypes | Done |
| F-010 | Drag & Drop Out | Drag cards from the panel to other apps via `onDrag` with `NSItemProvider` | Done |
| F-011 | File Bookmarks | Security-scoped bookmarks for persistent file access across app restarts | Done |
| F-012 | Clear All | Bulk-delete all items (preserves pinned items) | Done |
| F-013 | Delete Individual | Hover a card to reveal its delete button | Done |
| F-056 | Quick Paste | Double-click a card to copy content and paste it into the frontmost app (simulates ⌘V via CGEvent; requires Accessibility permission) | Done |
| F-057 | Hide Panel After Quick Paste Toggle | Settings toggle to keep the panel open after Quick Paste for consecutive pasting; uses `CGEvent.postToPid` to target the correct app when panel stays visible | Done |

### UI (Plan Step 8)

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-014 | Text Card | Displays text preview (max 5 lines), character & line counts | Done |
| F-015 | Image Card | Displays thumbnail (max 200pt height), dimensions & file size | Done |
| F-016 | File Card | Displays system file icon, file name & file size | Done |
| F-017 | Empty State | Centered placeholder with icon and guidance text when shelf is empty | Done |
| F-018 | Drop Zone Hint | Persistent "Drop or ⌘V to paste" hint at the bottom of the panel | Done |
| F-019 | Toast Notifications | Brief "Copied to clipboard" capsule toast feedback | Done |
| F-020 | Hover Effects | Scale (1.02x) + shadow + delete button appear on card hover | Done |
| F-021 | Text Selection | Text cards allow in-card text selection | Done |
| F-022 | Card Animations | Scale + opacity transitions on card insert and removal | Done |
| F-023 | Dark/Light Mode | UI automatically adapts to system appearance | Done |

### Settings (Plan Step 7)

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-024 | Auto-Monitor Toggle | Enable/disable clipboard background monitoring | Done |
| F-025 | Launch at Login | Toggle auto-start via macOS `SMAppService` API | Done |
| F-026 | Hotkey Customization | Record and set a custom global hotkey in Settings; dynamically re-registers via `UserDefaults` observation | Done |
| F-027 | In-App Language Switch | Choose English, Simplified Chinese, or Follow System; applies immediately without restart | Done |

### Source Tracking & UX Polish

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-058 | Source App Tracking | Records which application the content was copied from; displays app icon and name on each card via `SourceAppLabel` | Done |
| F-059 | Clear All Confirmation | Shows a native `NSAlert` confirmation dialog before bulk-deleting items | Done |
| F-060 | About Section | Settings shows app name, version, and description | Done |
| F-061 | Custom Cursor | Cards display a pointing-hand cursor on hover | Done |
| F-062 | Word Segmentation | Split text into selectable word chips via NLTokenizer; select chips to copy or create new cards. Especially useful for Chinese text where word boundaries aren't obvious | Done |

### Data & Persistence

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-028 | SwiftData Storage | Items persist across app restarts | Done |
| F-029 | External Image Storage | Image blobs stored outside SQLite via `@Attribute(.externalStorage)` | Done |
| F-030 | Pin Property | `isPinned` flag exists on `ShelfItem` model; pinned items survive "Clear All" | Partial |
| F-063 | App-Specific Storage Directory | SwiftData store located in `~/Library/Application Support/com.shelf.app/` via `StorageManager`; shared `ModelContainer` factory ensures a single container instance across the app | Done |

### Internationalization

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-031 | English Localization | Complete UI translation (40+ strings) | Done |
| F-032 | Chinese (Simplified) Localization | Complete UI translation (40+ strings) | Done |
| F-033 | Dynamic Bundle Switching | `Bundle.localizedBundle` checks `UserDefaults` and loads the matching `.lproj` sub-bundle at runtime | Done |

---

## TODO / Roadmap

> Features sourced from plan section "七、未来迭代 TODO" and gaps identified during implementation.

### High Priority

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-034 | Pin/Unpin UI | Pin button on card hover toggles `isPinned`; pinned cards sort to top with indicator icon | Done |
| F-036 | Search / Filter | Add a search bar to filter items by text content, file name, source app name, or tag name | Done |
| F-064 | Content Type Filter | Chip-based filter bar to filter items by content type (All/Text/Image/File); supports multi-select and combines with search and tag filters | Done |
| F-037 | Item Limit / Auto-Cleanup | Set a maximum number of stored items and auto-delete oldest entries | Done |

### Medium Priority

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-038 | Card Drag Reorder | Drag to reorder cards within the panel | TODO |
| F-039 | Inline Text Editing | Edit text content directly within a text card | TODO |
| F-040 | Rich Text Support | Preserve styled/attributed text from clipboard | TODO |
| F-041 | Favorites / Collections | Organize items with user-defined colored tags (up to 3 per item); filter by tag, manage via hover button, context menu, and Settings | Done |
| F-042 | Keyboard Navigation | Arrow keys to browse cards, Enter to copy, Delete to remove | Done |
| F-043 | Quick-paste by Index | ⌘1, ⌘2, … to paste the Nth card directly | Done |
| F-044 | Batch Operations | Multi-select cards for bulk delete or copy | TODO |
| F-045 | Context Menu | Right-click cards for copy, delete, pin, tags options | Done |
| F-046 | Panel Position Preference | Settings option for default panel position (left / right / top / bottom / free); top/bottom modes use horizontal card scrolling | Done |

### Low Priority

| ID | Feature | Description | Status |
|----|---------|-------------|--------|
| F-047 | Card Size Toggle | Switch between compact and expanded card display modes | TODO |
| F-048 | Menu Bar Quick Preview | Preview recent items from the menu bar dropdown without opening the panel | TODO |
| F-049 | URL Auto-Detection | Detect URLs in text and show link previews | TODO |
| F-050 | iCloud Sync | Sync shelf items across devices via CloudKit | TODO |
| F-051 | Snippet Templates | Save frequently-used text as reusable templates | TODO |
| F-052 | Export | Export shelf contents to a file (JSON, ZIP) | TODO |
| F-053 | Expanded Test Coverage | Add tests for services, ViewModel logic, and UI integration | TODO |
| F-054 | Additional Languages | Add more localizations (Japanese, Korean, etc.) | TODO |
| F-055 | Accessibility | VoiceOver labels, Dynamic Type support, keyboard-only navigation | TODO |
