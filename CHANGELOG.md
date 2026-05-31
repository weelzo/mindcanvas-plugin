# Changelog

All notable changes to this plugin are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/), and this project adheres to
[Semantic Versioning](https://semver.org/).

## [0.1.0] — 2026-05-31

Initial public release.

### Added
- `mindcanvas` MCP server connection over remote SSE, authenticated per-user via
  a session token stored in the OS keychain (`userConfig`).
- `mindcanvas` skill — Thinking Desk operating principles for reading and
  manipulating canvases.
- `/mindcanvas:mc-canvas` command — inspect a canvas (structure, breakdown,
  clusters, orphans).
- `/mindcanvas:mc-cleanup` command — reorganize a canvas live (cluster, link,
  summarize, seed).
- Self-contained marketplace (`marketplace.json`) for one-step install.
- 11 read/additive/modify tools: `list_canvases`, `list_nodes`, `list_edges`,
  `read_node`, `search_nodes`, `create_node`, `create_edge`, `update_node`,
  `move_node`, `resize_node`, `drop_seed`.

### Notes
- Phase 1 ships no destructive tools; deletions are deferred to Phase 2 with an
  approval queue.
