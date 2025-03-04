---
layout: ../../layouts/ProjectLayout.astro
title: "Telecharger :: youtube-dl TUI"
description: Telecharger is a Youtube-DL TUI. It provides the ability to build lists of videos you wish to download, rename the files, saving as audio only and a host of other functionality.
tags: ["cli", "go", "tool"]
githubUrl: https://github.com/jim-at-jibba/telecharger
timestamp: 2023-02-01T02:39:03+00:00
featured: false
filename: telecharger
---

# Telecharger

## A Modern Terminal UI for YouTube-DL

Telecharger is an elegant terminal-based user interface I built for [YouTube-DL](https://github.com/ytdl-org/youtube-dl), designed to streamline the video download workflow with a focus on usability and flexibility.

## Features

- **Queue Management**: Build and manage lists of videos for batch downloading
- **File Customization**: Easily rename output files without complex command flags
- **Format Options**: Toggle between video and audio-only downloads with a simple interface
- **Advanced Configuration**: Support for custom YouTube-DL flags through an intuitive form
- **Download History**: SQLite database persistence to track your download history
- **Cross-Platform**: Built in Go for excellent performance on macOS and Linux systems

## The Power of Simplicity

Telecharger transforms the YouTube-DL experience from memorizing complex command-line flags to a streamlined interface that makes media downloading accessible and efficient.

### Advanced Options Support

While keeping the interface clean, Telecharger provides full access to YouTube-DL's powerful options:

```
--add-metadata --write-all-thumbnails --embed-thumbnail --write-info-json --embed-subs --all-subs
```

## Technical Details

- **Architecture**: Built in Go for excellent performance and cross-platform compatibility
- **Data Storage**: SQLite database housed in a dedicated directory (`~/telecharger/`) for persistent history
- **Dependencies**:
  - [YouTube-DL](https://github.com/ytdl-org/youtube-dl)
  - [FFMPEG](https://ffmpeg.org/) for media processing

## Installation

```sh
go install github.com/jim-at-jibba/telecharger@latest
```

## Usage

Simply run:

```sh
telecharger
```

## Development Approach

With Telecharger, I wanted to create a tool that makes YouTube-DL more accessible while preserving its powerful functionality. Key development considerations included:

- **User Experience**: Creating an intuitive TUI that doesn't require reading documentation
- **Progressive Disclosure**: Simple by default, but with full power available when needed
- **Persistence**: Saving download history for future reference
- **Performance**: Using Go for a fast, responsive terminal experience

## Future Enhancements

The next development phase will include configuration management within the same `~/telecharger` directory structure, providing users with even more customization options.

## Project Status

Telecharger is fully functional for most YouTube-DL use cases. While it doesn't yet support every flag available in the core tool, the most commonly used options are available, and additional flags can be specified manually through the interface.

---

[View Telecharger on GitHub](https://github.com/jim-at-jibba/dtc)
