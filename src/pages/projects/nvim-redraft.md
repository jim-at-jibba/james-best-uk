---
layout: ../../layouts/ProjectLayout.astro
title: "nvim-redraft :: AI-Powered Inline Code Editing"
description: A Neovim plugin for seamless AI-powered inline code editing with support for multiple LLM providers.
tags: ["neovim", "ai", "lua", "typescript", "plugin"]
timestamp: 2025-10-06T00:00:00+00:00
featured: true
filename: nvim-redraft
---

# nvim-redraft

## AI-Powered Inline Code Editing for Neovim

nvim-redraft is a Neovim plugin I developed that brings seamless AI-powered code editing directly into your workflow. This tool enables developers to select code in visual mode and apply AI-driven transformations inline, without interrupting their editing flow or dealing with confirmation dialogs.

[View on GitHub](https://github.com/jim-at-jibba/nvim-redraft)

## The Problem I Solved

Modern AI coding assistants often require context switching—copying code to external tools, waiting for responses, and manually pasting results back. This friction breaks developer flow. nvim-redraft eliminates this disruption by embedding AI capabilities directly into Neovim, allowing developers to edit code naturally through visual selection and concise instructions.

## Key Features

### Frictionless Editing Experience

I designed nvim-redraft to prioritize speed and minimal disruption:

- Visual mode selection integration
- No confirmation dialogs—immediate inline editing
- Customizable keybindings for personalized workflows
- Seamless integration with existing Neovim configurations

### Multi-Provider LLM Support

The plugin supports flexibility in AI provider choice:

- OpenAI (GPT-4o, GPT-4o-mini)
- Anthropic (Claude 3.5 Sonnet, Claude 3.7 Sonnet)
- xAI (Grok models)
- Configurable model selection for each provider
- Adjustable timeout settings for large code selections

### Developer-Centric Design

Built with performance and usability in mind:

- Hybrid Lua/TypeScript architecture for optimal performance
- Customizable system prompts for specific coding styles
- Debug logging for troubleshooting and transparency
- Secure API key management through environment variables

## Technical Implementation

nvim-redraft combines several technologies for efficient operation:

- Lua core for Neovim integration and event handling
- TypeScript service for AI provider communication
- Sparse edit transformation for precise code modifications
- Asynchronous processing to prevent editor blocking
- Integration with snacks.nvim for user input handling

## User Workflow

I designed nvim-redraft around a natural editing flow:

1. **Select**: Highlight code in visual mode (`v`, `V`, or `Ctrl-v`)
2. **Invoke**: Press `<leader>ae` (or your configured keybinding)
3. **Instruct**: Enter a concise editing instruction
4. **Apply**: AI-generated changes appear inline immediately

## Unique Value Proposition

What sets nvim-redraft apart from other AI coding tools:

- **Zero Context Switching**: Edit code without leaving Neovim
- **Provider Flexibility**: Choose the AI provider that fits your needs
- **No Subscriptions**: Use your own API keys with pay-per-use pricing
- **Performance Optimized**: Built with Lua and TypeScript for speed
- **Highly Configurable**: Customize prompts, keybindings, and behavior
- **Privacy-Focused**: No data collection beyond API communication

## Development Status

nvim-redraft is actively maintained and production-ready:

- Stable release available for installation
- Support for Neovim 0.8.0 and later
- Comprehensive documentation and troubleshooting guides
- Active issue tracking and feature development on GitHub

## Future Development Roadmap

The next phases of nvim-redraft development will include:

- Support for additional LLM providers
- Context-aware editing with project-specific knowledge
- Multi-file refactoring capabilities
- Template-based code generation
- Enhanced debugging and logging features

