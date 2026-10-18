---
layout: ../../layouts/ProjectLayout.astro
title: "nvim-stride :: AI-Powered Next-Edit Predictions"
description: A Neovim plugin that predicts where you'll edit next based on recent changes, with support for intelligent refactoring and ghost text completions.
tags: ["neovim", "ai", "lua", "refactoring", "plugin"]
githubUrl: https://github.com/jim-at-jibba/nvim-stride
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
- Multi-edit predictions: a rename touching several call sites is predicted in a single request, and `Tab` steps through the edits with a `[n/m]` counter
- Automatic triggering on `InsertLeave` and normal mode edits
- Remote suggestions with strikethrough highlighting for replaced text
- Insert detection for new parameters, properties, or arguments
- Incremental change tracking via `nvim_buf_attach`
- Simple dismissal with `Esc` or `:StrideClear`

### Ghost Text Completion Mode

Complementary inline completions for faster coding:

- Real-time ghost text suggestions as you type
- Suggestion retention: keep typing and characters matching the ghost text are consumed without a new request
- Partial accepts for the next word (`<M-w>`) or first line (`<M-l>`) of a suggestion
- Focused completions that target the current statement or expression, keeping them fast and non-intrusive
- Comment-intent completion: type `// log the id` and get `console.log(id)`
- Treesitter-aware context capture for accurate completions
- Project context: include rules from files like `AGENTS.md` in prompts
- Tab-to-accept workflow integration

### Developer-Centric UX

Seamless integration with existing workflows:

- Configurable debounce timing (500ms default)
- Customizable keybindings for accept, partial accept and dismiss
- Gutter icon indicator when suggestions are active
- Global enable/disable commands (`:StrideEnable`, `:StrideDisable`)
- `:StrideStatus` to inspect the active suggestion and connection state
- Automatic race condition handling for concurrent edits
- Bottom-center notifications showing which direction the next suggestion is in
## Technical Implementation

nvim-stride leverages several technologies for intelligent prediction:

- Lua core for Neovim integration and real-time event handling
- `nvim_buf_attach` with `on_bytes` callback for incremental edit tracking
- Treesitter integration for semantic context awareness
- Cerebras API for ultra-low latency inference
- Shared transport layer with real request cancellation, throttling and 429 backoff
- Word-level diffs and deduplicated context to keep prompts small
- Token budget management for efficient prompt construction
- Smart context extraction with configurable line limits
- Deterministic completion caching

### Architecture Highlights

What makes stride's prediction engine different:

- **Incremental Tracking** - Real-time edit capture without blocking the editor, storing buffer state incrementally rather than full snapshots per keystroke
- **Smart Context** - Treesitter-powered context expansion for accurate predictions
- **Token Budgeting** - Automatic history trimming to stay within model limits
- **Dual Mode Design** - Completion and refactor modes can run simultaneously
- **Race Protection** - Stale responses discarded if cursor has moved
- **Rate-Limit Aware** - Honors `Retry-After` on 429s and kills in-flight requests on cancel so no tokens are wasted
- **Remote Rendering** - Preview changes inline without applying them
## User Workflow

### Completion Mode

1. **Type** - Start coding in insert mode
2. **Pause** - After 500ms, ghost text suggestion appears
3. **Accept** - Press `Tab` to accept the suggestion, or `<M-w>` / `<M-l>` to accept just the next word or line
4. **Continue** - Any other key dismisses and resumes typing

### Refactor Mode

1. **Edit** - Make a change (e.g., rename a variable)
2. **Exit** - Leave insert mode to trigger prediction
3. **Review** - Related edits shown with strikethrough and replacement preview
4. **Apply** - Press `Tab` to accept and step to the next predicted edit, or `Esc` to dismiss
## Configuration & Integration

### Customization Options

Stride offers extensive customization:

- API endpoint and model selection
- Debounce timing and context window size
- Rate limiting: minimum request interval and cooldown after a 429
- Project context files such as `AGENTS.md`
- Mode selection (completion, refactor, or both)
- Filetype exclusions for specific workflows
- Custom highlight groups for visual consistency
- Token budget and change history limits
- Gutter sign customization or disabling

### Tool Integration

Works alongside existing tools:

- **blink.cmp** - Smart Tab key handling with priority checking
- **snacks.nvim** - Animated fade in/out for notifications
- **fidget.nvim** - Optional notification backend
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
- Additional LLM provider support

## Why nvim-stride?

What sets stride apart from traditional refactoring tools:

- **Context-Aware** - Understands coding patterns, not just text matching
- **Non-Intrusive** - Suggestions appear only when relevant
- **Ultra-Fast** - Powered by Cerebras for minimal latency
- **Full Control** - Review before applying, dismiss anytime
- **Dual Mode** - Completion and refactoring in one plugin
- **Open Source** - MIT licensed with transparent implementation
