# Changelog

Notable changes to this project will be documented in this file.

## Distribution

- **Source Code:** [LM Studio Hub](https://lmstudio.ai/ceveyne/draw-things-index/revisions)
- **Documentation:** [GitHub Repository](https://github.com/ceveyne/draw-things-index-docs)

## [0.1.0] - 2026-01-26 Revision 5

### Added

- Enhanced search results for easier parameter reuse based on former image generations.
- Added ComfyUI PNG metadata support (reads workflow/prompt from saved PNG).

### Changed

- Improved search results for similar images from different sources.
- Updated user documentation to reflect the recent changes.

---

## [0.1.0] - 2026-01-23 Revision 4

### Changed

- Improved Semantic Search settings for short queries.

---

## [0.1.0] - 2026-01-22 Revision 3

### Fixed

- `retrievalLimit` setting now works more strictly (Agent model can no longer override).
- Project files now return all image variants for a queried prompt.

---

## [0.1.0] - 2026-01-22 Revision 2

### Added

- Small additions to the user documentation.

### Fixed

- Project file parser now extracts all image variants.

---

## [0.1.0] - 2026-01-21 - Revision 1

### Added

- Initial release
- LM Studio Plugin to search through your Draw Things generation history
- Multi-source indexing (**draw-things-chat** generation logs, PNGs from former generations, Chat attachments, Draw Things projects files)
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
