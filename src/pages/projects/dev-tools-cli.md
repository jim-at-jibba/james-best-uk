---
layout: ../../layouts/ProjectLayout.astro
title: "DTC :: CLI package"
description: A collection of tools that you would normally reach to a browser for.
tags: ["cli", "go", "open-source", "tool"]
githubUrl: https://github.com/jim-at-jibba/dtc
timestamp: 2024-11-24T02:39:03+00:00
featured: false
filename: dev-tools-cli
---

# DTC: Developer's Terminal Companion

DTC is a powerful command-line utility designed to streamline common development tasks directly from your terminal. Built with Go and leveraging the elegant UI capabilities of Charm's suite of tools, DTC brings efficiency and style to your workflow.

## Core Technologies

DTC is crafted using:

- Go programming language
- Cobra command framework
- Charm's beautiful terminal UI libraries:
  - [Bubbletea](https://github.com/charmbracelet/bubbletea) - Terminal UI framework
  - [Lipgloss](https://github.com/charmbracelet/lipgloss) - Style definitions for terminal applications
  - [Bubbles](https://github.com/charmbracelet/bubbles) - Common UI components for terminal apps

## Installation

Get started with a single command:

```sh
go install github.com/jim-at-jibba/dtc@latest
```

## Feature Highlights

### UUID Generation

Generate UUIDs with automatic clipboard copying:

```bash
# Generate a single UUID
dtc uuid generate

# Generate multiple UUIDs
dtc uuid generate --count=100
```

### Base64 Encoding & Decoding

Handle Base64 operations in both standard and URL-compatible formats:

```bash
# Encode in standard format
dtc base64 encode

# Encode in URL-compatible format
dtc base64 encode -u

# Decode from standard format
dtc base64 decode

# Decode from URL-compatible format
dtc base64 decode -u
```

### Ephemeral File Sharing

Share files securely with automatic expiration via [file.io](https://file.io):

```bash
# Share with default 14-day expiry
dtc file-share

# Custom expiration periods
dtc file-share --expiry=3d  # 3 days
dtc file-share --expiry=4w  # 4 weeks
```

Note: 100MB file size limit applies.

### JWT Debugger

Inspect and analyze JWT tokens directly in your terminal:

```bash
dtc jwt-debugger
```

## Discover More

Visit the [DTC Repository](https://github.com/jim-at-jibba/dtc) to explore all features and see DTC in action.
