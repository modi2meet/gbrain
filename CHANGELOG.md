# Changelog

All notable changes to GBrain will be documented in this file.

## [0.2.0.2] - 2026-04-07

### Changed

- Rewrote recommended brain schema doc with expanded architecture: database layer (entity registry, event ledger, fact store, relationship graph) presented as the core architecture, entity identity and deduplication, enrichment source ordering, epistemic discipline rules, worked examples showing full ingestion chains, concurrency guidance, and browser budget. Smoothed language for open-source readability.

## [0.2.0.1] - 2026-04-07

### Added

- Recommended brain schema doc (`docs/GBRAIN_RECOMMENDED_SCHEMA.md`): full MECE directory structure, compiled truth + timeline pages, enrichment pipeline, resolver decision tree, skill architecture, and cron job recommendations. The OpenClaw paste now links to this as step 5.

### Changed

- First-time experience rewritten. "Try it" section shows your own data, not fictional PG essays. OpenClaw paste references the GitHub repo, includes bun install fallback, and has the agent pick a dynamic query based on what it imported.
- Removed all references to `data/kindling/` (a demo corpus directory that never existed).

## [0.2.0] - 2026-04-05

### Added

- You can now keep your brain current with `gbrain sync`, which uses git's own diff machinery to process only what changed. No more 30-second full directory walks when 3 files changed.
- Watch mode (`gbrain sync --watch`) polls for changes and syncs automatically. Set it and forget it.
- Binary file management with `gbrain files` commands (list, upload, sync, verify). Store images, PDFs, and audio in Supabase Storage instead of clogging your git repo.
- Install skill (`skills/install/SKILL.md`) that walks you through setup from scratch, including Supabase CLI magic path for zero-copy-paste onboarding.
- Import and sync now share a checkpoint. Run `gbrain import`, then `gbrain sync`, and it picks up right where import left off. Zero gap.
- Tag reconciliation on reimport. If you remove a tag from your markdown, it actually gets removed from the database now.
- `gbrain config show` redacts database passwords so you can safely share your config.
- `updateSlug` engine method preserves page identity (page_id, chunks, embeddings) across renames. Zero re-embedding cost.
- `sync_brain` MCP tool returns structured results so agents know exactly what changed.
- 20 new sync tests (39 total across 3 test files)

## [0.1.0] - 2026-04-05

### Added

- Pluggable engine interface (`BrainEngine`) with full Postgres + pgvector implementation
- 25+ CLI commands: init, get, put, delete, list, search, query, import, export, embed, stats, health, link/unlink/backlinks/graph, tag/untag/tags, timeline/timeline-add, history/revert, config, upgrade, serve, call
- MCP stdio server with 20 tools mirroring all CLI operations
- 3-tier chunking: recursive (delimiter-aware), semantic (Savitzky-Golay boundary detection), LLM-guided (Claude Haiku topic shifts)
- Hybrid search with Reciprocal Rank Fusion merging vector + keyword results
- Multi-query expansion via Claude Haiku (2 alternative phrasings per query)
- 4-layer dedup pipeline: by source, cosine similarity, type diversity, per-page cap
- OpenAI embedding service (text-embedding-3-large, 1536 dims) with batch support and exponential backoff
- Postgres schema with pgvector HNSW, tsvector (trigger-based, spans timeline_entries), pg_trgm fuzzy slug matching
- Smart slug resolution for reads (fuzzy match via pg_trgm)
- Page version control with snapshot, history, and revert
- Typed links with recursive CTE graph traversal (max depth configurable)
- Brain health dashboard (embed coverage, stale pages, orphans, dead links)
- Stale alert annotations in search results
- Supabase init wizard with CLI auto-provision fallback
- Slug validation to prevent path traversal on export
- 6 fat markdown skills: ingest, query, maintain, enrich, briefing, migrate
- ClawHub manifest for skill distribution
- Full design docs: GBRAIN_V0 spec, pluggable engine architecture, SQLite engine plan
