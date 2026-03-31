# Changelog

Notable changes to this project will be documented in this file.

## Distribution

- **Source Code:** [LM Studio Hub](https://lmstudio.ai/ceveyne/draw-things-index/revisions)
- **Documentation:** [GitHub Repository](https://github.com/ceveyne/draw-things-index-docs)

---

## [0.1.12] - 2026-04-01 Revision 11/12

### Changed

- Extended FlatBuffers schema for future use.

---

## [0.1.10] - 2026-03-13 Revision 10

### Added

- Added Support for modes `text2video` and `image2video`.

### Fixed

- Project file parser now reads SQLite WAL (Write-Ahead Log) data. Draw Things uses WAL journaling mode, causing recent generations to be invisible to the previous `sql.js`-only reader. The parser now detects `-wal` sidecar files and uses native `sqlite3 VACUUM INTO` to create a merged temporary copy before parsing.

---

## [0.1.9] - 2026-03-11 Revision 9

### Changed

- Search results now alternate between different source types for more variety.
- Project file parsing skips non-generated entries and deduplicates LoRAs.

---

## [0.1.8] - 2026-02-08 Revision 8

### Changed

- Improved search results for metadata-related queries (size, model, LoRAs, source, project, timestamp).

---

## [0.1.7] - 2026-02-01 Revision 7

### Added

- Added multiple folder support for images with embedded metadata (Draw Things XMP, ComfyUI prompt JSON).

---

## [0.1.6] - 2026-01-29 Revision 6

### Added

- New screenshots to reflect the recent update to LM Studio 0.4.0.

---

## [0.1.5] - 2026-01-26 Revision 5

### Added

- Enhanced search results for easier parameter reuse based on former image generations.
- Added ComfyUI PNG metadata support (reads workflow/prompt from saved PNG).

### Changed

- Improved search results for similar images from different sources.
- Updated user documentation to reflect the recent changes.

---

## [0.1.4] - 2026-01-23 Revision 4

### Changed

- Improved Semantic Search settings for short queries.

---

## [0.1.3] - 2026-01-22 Revision 3

### Fixed

- `retrievalLimit` setting now works more strictly (Agent model can no longer override).
- Project files now return all image variants for a queried prompt.

---

## [0.1.2] - 2026-01-22 Revision 2

### Added

- Small additions to the user documentation.

### Fixed

- Project file parser now extracts all image variants (was missing regenerations with pk1 > 1).

---

## [0.1.1] - 2026-01-21 Revision 1

### Added

- Initial release
- LM Studio Plugin to search through your Draw Things generation history
- Multi-source indexing (**draw-things-chat** generation logs, PNGs from former generations, Chat attachments, Draw Things project files)
- Reactive file watchers (instant cache invalidation)
- Word-boundary matching
- English stemming (cats→cat, running→run)
- Fuzzy matching (Levenshtein for typos)
- Dead link filtering
- Source tracking (know where each match came from)
- Project URI scheme for on-demand thumbnail extraction
- **Semantic Search** - Cross-language search with multilingual embeddings
  - "Katze" → finds "cat" prompts
  - "Sonnenuntergang" → finds "sunset", "golden hour"
  - Synonym matching ("auto" → "car", "vehicle")
  - Persisted embeddings (no re-embedding on restart)
