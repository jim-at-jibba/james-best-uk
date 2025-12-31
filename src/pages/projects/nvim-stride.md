---
layout: ../../layouts/ProjectLayout.astro
title: "nvim-stride :: AI-Powered Next-Edit Predictions"
description: A Neovim plugin that predicts where you'll edit next based on recent changes, with support for intelligent refactoring and ghost text completions.
tags: ["neovim", "ai", "lua", "refactoring", "plugin"]
timestamp: 2025-12-31T00:00:00+00:00
featured: true
filename: nvim-stride
---

## nvim-stride

### AI-Powered Next-Edit Suggestions for Neovim

nvim-stride is a Neovim plugin that brings intelligent next-edit prediction directly into your workflow. It analyzes recent code changes and predicts where you'll edit next—rename a variable on line 10, and stride suggests updating line 50. This eliminates tedious manual search-and-replace while maintaining full developer control.

[View on GitHub](https://github.com/jim-at-jibba/nvim-stride)

## The Problem

During refactoring sessions, developers make related changes across multiple locations. Traditional find-and-replace is blunt and risky, while manually tracking every related edit is tedious and error-prone. nvim-stride bridges this gap by intelligently predicting related edits based on coding patterns, suggesting changes only where they're contextually relevant.
## Key Features

### Intelligent Refactor Mode

Stride's refactor mode understands the intent behind edits:

- Next-edit prediction based on recent changes
- Automatic triggering on `InsertLeave` and normal mode edits
- Remote suggestions with strikethrough highlighting for replaced text
- Insert detection for new parameters, properties, or arguments
- Incremental change tracking via `nvim_buf_attach`
- Simple dismissal with `Esc` or `:StrideClear`

### Ghost Text Completion Mode

Complementary inline completions for faster coding:

- Real-time ghost text suggestions as you type
- Treesitter-aware context capture for accurate completions
- Multi-line suggestion support
- Tab-to-accept workflow integration

### Developer-Centric UX

Seamless integration with existing workflows:

- Configurable debounce timing (300ms default)
- Customizable keybindings for accept and dismiss
- Gutter icon indicator when suggestions are active
- Global enable/disable commands (`:StrideEnable`, `:StrideDisable`)
- Automatic race condition handling for concurrent edits
- Optional fidget.nvim integration for non-intrusive notifications
## Technical Implementation

nvim-stride leverages several technologies for intelligent prediction:

- Lua core for Neovim integration and real-time event handling
- `nvim_buf_attach` with `on_bytes` callback for incremental edit tracking
- Treesitter integration for semantic context awareness
- Cerebras API for ultra-low latency inference
- Token budget management for efficient prompt construction
- Smart context extraction with configurable line limits

### Architecture Highlights

What makes stride's prediction engine different:

- **Incremental Tracking** - Real-time edit capture without blocking the editor
- **Smart Context** - Treesitter-powered context expansion for accurate predictions
- **Token Budgeting** - Automatic history trimming to stay within model limits
- **Dual Mode Design** - Completion and refactor modes can run simultaneously
- **Race Protection** - Stale responses discarded if cursor has moved
- **Remote Rendering** - Preview changes inline without applying them
## User Workflow

### Completion Mode

1. **Type** - Start coding in insert mode
2. **Pause** - After 300ms, ghost text suggestion appears
3. **Accept** - Press `Tab` to accept the suggestion
4. **Continue** - Any other key dismisses and resumes typing

### Refactor Mode

1. **Edit** - Make a change (e.g., rename a variable)
2. **Exit** - Leave insert mode to trigger prediction
3. **Review** - Related edits shown with strikethrough and replacement preview
4. **Apply** - Press `Tab` to accept or `Esc` to dismiss
## Configuration & Integration

### Customization Options

Stride offers extensive customization:

- API endpoint and model selection
- Debounce timing and context window size
- Mode selection (completion, refactor, or both)
- Filetype exclusions for specific workflows
- Custom highlight groups for visual consistency
- Token budget and change history limits
- Gutter sign customization or disabling

### Tool Integration

Works alongside existing tools:

- **blink.cmp** - Smart Tab key handling with priority checking
- **fidget.nvim** - Auto-detected non-intrusive notifications
- **nvim-treesitter** - Optional semantic context enhancement
- **plenary.nvim** - Reliable async operations
## Development & Roadmap

### Current Status

nvim-stride is under active development:

- Early release with stable core features
- Support for Neovim 0.10+
- Comprehensive documentation and examples
- Open to feedback and bug reports

### Future Enhancements

Planned improvements include:

- LSP integration for diagnostics and symbol awareness
- Enhanced Treesitter integration for scope-aware predictions
- Multi-file context awareness for project-wide refactoring
- Custom prompt templates for specialized workflows
- Prediction caching for improved performance
- Additional LLM provider support

## Why nvim-stride?

What sets stride apart from traditional refactoring tools:

- **Context-Aware** - Understands coding patterns, not just text matching
- **Non-Intrusive** - Suggestions appear only when relevant
- **Ultra-Fast** - Powered by Cerebras for minimal latency
- **Full Control** - Review before applying, dismiss anytime
- **Dual Mode** - Completion and refactoring in one plugin
- **Open Source** - MIT licensed with transparent implementation
