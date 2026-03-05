---
layout: ../../layouts/ProjectLayout.astro
title: "qmdf :: Lightning-Fast Markdown Search in Your Terminal"
description: A keyboard-driven Go TUI for searching and managing qmd Markdown collections with live preview, semantic search, and seamless editor handoff.
tags: ["go", "tui", "bubbletea", "markdown", "cli"]
githubUrl: https://github.com/jim-at-jibba/qmdf
timestamp: 2026-02-27T00:00:00+00:00
featured: true
filename: qmdf
---

# qmdf

## Fast, Keyboard-First Markdown Search for Power Users

qmdf is a lightweight terminal UI that wraps the `qmd` CLI and turns Markdown search into a fluid, interactive workflow. Instead of bouncing between commands, files, and tools, you can search, preview, and open documents from one interface.

It ships as a single static binary with sub-10ms startup and no runtime dependencies.

[View on GitHub](https://github.com/jim-at-jibba/qmdf)

## The Problem

Raw CLI search is powerful, but real-world note workflows involve more than searching: previewing content, switching retrieval modes, opening files, and managing collections. Doing that across multiple commands creates friction and context switching.

qmdf closes that gap with a focused TUI that keeps the entire search-to-edit loop in one place.

## Key Features

### Live Search Across Three Retrieval Modes

qmdf supports multiple discovery strategies without leaving the keyboard:

- `search` for classic full-text retrieval
- `vsearch` for semantic/vector search
- `query` for LLM-reranked results
- 150ms debounced input for responsive typing
- Stale-response protection via monotonic request IDs

### Two-Pane Workflow Optimized for Speed

A practical layout designed for scanning and acting quickly:

- Left pane for ranked results
- Right pane for rendered Markdown preview
- Open selected file in `$EDITOR` (`enter` / `e`)
- Open in `$PAGER` (`ctrl+p`)
- Copy path (`ctrl+y`) or doc ID (`ctrl+i`) instantly

### Built-In Collection Management

qmdf handles operational knowledge-base workflows as well:

- Add, rename, and delete collections
- Reindex collections (`qmd update`, with optional `--pull`)
- Generate embeddings (`qmd embed`, including force mode)
- Manage collection contexts for LLM-aware query behavior

## Technical Implementation

qmdf is implemented in Go using modern terminal UI tooling:

- **Cobra** for command and flag handling
- **Bubble Tea** for event-driven TUI architecture
- **Lip Gloss** for layout and styling
- **Glamour** for Markdown rendering
- **Viper** for config and environment variable support

### Architecture Highlights

What keeps qmdf fast and reliable:

- Defensive `qmd` JSON parsing supporting both wrapped and bare result arrays
- Preview cache with FIFO eviction (20 entries)
- Editor handoff through `tea.ExecProcess` for clean terminal control
- Mode-aware timeout strategy, including longer waits for LLM-heavy query mode

## User Workflow

### Search and Open

1. Launch `qmdf`
2. Type a query and cycle modes with `tab`
3. Navigate results with arrows or `j/k`
4. Open the selected result directly in your editor

### Shell Integration

Use `--print` to compose qmdf into scripts and shell workflows:

```bash
$EDITOR "$(qmdf --print)"
cd "$(dirname "$(qmdf --print)")"
```

## Configuration & Integration

### Flexible Defaults

`~/.config/qmdf/config.yaml` supports:

- Default collection and mode
- Result limits and minimum score
- Preview toggle and split width
- Editor overrides (including env-prefixed commands)

All settings are also available as `QMDF_` environment variables for scriptable workflows.

## Development Status

qmdf is actively maintained and ready for daily use:

- Production-ready core search and preview workflows
- Cross-platform builds for macOS, Linux, and Windows
- Automated release pipeline via GitHub Actions and GoReleaser
- MIT licensed and open source

## Why qmdf?

- Fast: near-instant startup and responsive search UX
- Focused: keyboard-first interface for terminal-native workflows
- Flexible: full-text, semantic, and LLM-reranked retrieval in one tool
- Practical: search, preview, open, and manage collections without context switching
- Portable: single static binary with zero runtime dependencies
