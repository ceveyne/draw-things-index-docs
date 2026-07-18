# Changelog

Notable changes to this project will be documented in this file.

## Distribution

- **Source Code:** [LM Studio Hub](https://lmstudio.ai/ceveyne/draw-things-index/revisions)
- **Documentation:** [GitHub Repository](https://github.com/ceveyne/draw-things-index-docs)

---

## [0.1.22] - 2026-07-18 Revision 22

### Fixed

- Draw Things projects are no longer modified during indexing.

---

## [0.1.21] - 2026-07-17 Revision 21

### Changed

- Improved Draw Things project-file thumbnail import compatibility.

---

## [0.1.20] - 2026-07-09 Revision 20

### Fixed

- Declared `flatbuffers` as an explicit dependency in `package.json`.

---

## [0.1.19] - 2026-07-09 Revision 19

### Changed

- Moved persistent index data from the plugin-local `data/` directory to `~/.draw-things-index`, so plugin updates no longer remove cached embeddings or project metadata.
- Reused cached Draw Things project metadata across plugin restarts, reducing repeated project parsing for unchanged `.sqlite3` files.
- Improved `index_image` reliability during overlapping index runs and made media-handle queries (`aN`, `vN`, `iN`, `pN`) resolve more consistently.

---

## [0.1.18] - 2026-06-02 Revision 18

### Changed

- Optimized semantic search parameters.

---

## [0.1.17] - 2026-05-26 Revision 17

### Added

- `index_image` now accepts a Draw Things project filename (e.g. `"my-project.sqlite3"`) as query and returns all generations from that project in chronological order. Results are not filtered by `retrievalLimit` and semantic search is skipped for these queries.

---

## [0.1.15] - 2026-05-24 Revision 16

### Changed

- Dead-link filtering now runs before the `retrievalLimit` slice in `searchGenerations`. Previously, a top-scoring generation whose image files were missing would consume one of the top-N slots and lower-ranked alive generations would never surface. With this change, `retrievalLimit=5` returns up to 5 generations whose images still exist on disk.
- Optimized multi-term queries: synonym lists no longer return fewer hits than a single-term subset. Default `minMatchScore` lowered from 70 to 65 so partial matches in long queries pass the threshold.

---

## [0.1.15] - 2026-04-24 Revision 15

### Added

- Added LITX-2.3 1.1 model family.
- Added 8-bit S (`i8x`) model filenames for Z Image, Qwen Image, Qwen Edit, FLUX.2 [klein] 4B, and LTX-2.3.

---

## [0.1.14] - 2026-04-08 Revision 14

### Changed

- Changed default image directory to `.lmstudio/working-directories`. Useful if "Embed Metadata in PNGs" is enabled in `draw-things-chat`.

---

## [0.1.13] - 2026-04-04 Revision 13

### Added

- Index notation support in `query`: `aN`, `vN`, `iN`, `pN` are automatically resolved to filenames before searching (e.g., "a1" finds the image by the filename of attachment 1).

### Changed

- `jsonlLogsDirectories` setting (replaces `jsonlLogsDirectory`) now accepts an array of log folder paths, allowing audit logs from multiple plugins to be indexed.

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
