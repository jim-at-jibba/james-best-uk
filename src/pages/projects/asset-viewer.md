---
layout: ../../layouts/ProjectLayout.astro
title: "Asset Viewer :: Desktop Application"
description: A desktop application for game developers to view, organize, and preview 2D sprite assets and audio files.
tags: ["electron", "gamedev", "tool", "typescript", "react"]
githubUrl: https://github.com/jim-at-jibba/2d-asset-viewer
timestamp: 2025-05-12T02:39:03+00:00
featured: true
filename: asset-viewer
---

# Asset Viewer

## A Streamlined Development Asset Manager

Asset Viewer is a desktop application I built to help game developers efficiently view, organize, and preview their 2D sprite assets and audio files. It addresses the common workflow challenge of quickly inspecting game assets without launching resource-intensive game engines or graphics programs.

## Core Features

### Visual Asset Management

The application provides a clean, intuitive interface for:

- **File System Navigation**: Browse your project directories with familiar navigation patterns
- **Asset Preview**: View sprites and textures with full transparency support
- **Animation Detection**: Automatically identify and organize animation sequences
- **Sprite Sheet Support**: View and extract individual sprites from sprite sheets
- **Animation Playback**: Play animation sequences directly within the application

### Audio Support

Asset Viewer handles multiple audio formats:

- MP3, WAV, OGG, M4A, and FLAC files
- Basic playback controls
- Audio waveform visualization
- Metadata display

### Workflow Optimization

I designed Asset Viewer with workflow efficiency in mind:

- **Asset Grid**: View multiple assets simultaneously in a customizable grid layout
- **Drag and Drop**: Seamlessly drag files into the application for quick viewing
- **Recent Files**: Quickly access your most recently viewed assets
- **Minimal UI**: Focus on your assets with a clean, distraction-free interface

## Technical Implementation

Asset Viewer combines several powerful technologies:

- **Electron**: Cross-platform desktop application framework
- **React + TypeScript**: For a robust, type-safe UI
- **Tailwind CSS**: Utility-first CSS framework for consistent styling
- **Radix UI**: Accessible UI component system
- **electron-vite**: Modern build tooling for Electron applications

## Development Approach

This project was built with a focus on:

- **Performance**: Fast loading and rendering, even with large asset collections
- **Simplicity**: Keeping the UI intuitive and focused on essential functionality
- **Developer Experience**: Creating a tool I would want to use in my own workflow

## Project Status

Asset Viewer was built through "vibe coding" - a process of rapidly building something that solves an immediate need. The application is offered as-is, and I won't be actively developing it further unless I personally need additional features.

If you find Asset Viewer useful and want to extend its functionality, pull requests are welcome!

## Getting Started

To run Asset Viewer locally:

```bash
# Clone the repository
git clone https://github.com/jim-at-jibba/2d-asset-viewer.git

# Install dependencies (npm)
cd 2d-asset-viewer
npm install

# Or using pnpm (preferred)
cd 2d-asset-viewer
pnpm install

# Start the application with npm
npm run dev

# Or start with pnpm (preferred)
pnpm dev
```

## Usage Example

Asset Viewer works best when pointed at your game project's asset directory:

1. Launch the application
2. Navigate to your project's sprite or audio directories
3. Click on assets to preview them in the main panel
4. For animations, use the playback controls to view the sequence
5. Drag and drop files directly into the application for quick viewing
