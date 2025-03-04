---
layout: ../../layouts/ProjectLayout.astro
title: "Micropython.nvim :: Neovim Plugin"
description: A Neovim plugin for working with Micropython projects.
tags: ["lua", "neovim", "micropython", "tool"]
githubUrl: https://github.com/jim-at-jibba/micropython.nvim
timestamp: 2024-03-19T02:39:03+00:00
featured: true
filename: micropython
---

# micropython_nvim

## Streamlined MicroPython Development Inside Neovim

micropython_nvim is a powerful Neovim plugin I created to enhance the MicroPython development experience. It brings the convenience of modern development workflows to microcontroller programming, allowing you to run code, manage files, and access the REPL without ever leaving your editor.

### Key Features

- **Seamless Code Execution**: Run your Python files directly on your microcontroller with a single command
- **Simplified File Management**: Upload individual files or entire projects with intelligent file filtering
- **Integrated REPL Access**: Interact with your device's REPL inside Neovim
- **Smart Project Setup**: Initialize new projects with sensible defaults and required configuration
- **Device Configuration**: Easily manage connection settings like port and baud rate
- **Statusline Integration**: See your connection status at a glance

## Getting Started

### Prerequisites

- Neovim 0.9 or higher
- [toggleterm.nvim](https://github.com/akinsho/toggleterm.nvim)
- [dressing.nvim](https://github.com/stevearc/dressing.nvim) (optional, for enhanced UI)
- Adafruit ampy
- rshell

### Installation

Using lazy.nvim:

```lua
{
    "jim-at-jibba/micropython.nvim",
    dependencies = { "akinsho/toggleterm.nvim", "stevearc/dressing.nvim" },
}
```

### Basic Configuration

Add a keybinding to run your code:

```lua
vim.keymap.set("n", "<leader>mr", require("micropython_nvim").run)
```

For the best experience, add the status component to your statusline:

```lua
require("lualine").setup({
    sections = {
        lualine_b = {
            {
              require("micropython_nvim").statusline,
              cond = package.loaded["micropython_nvim"] and require("micropython_nvim").exists,
            },
        }
    }
})
```

## Core Commands

| Command        | Description                                     |
| -------------- | ----------------------------------------------- |
| `:MPRun`       | Run current buffer on the microcontroller       |
| `:MPSetPort`   | Configure the connection port                   |
| `:MPSetBaud`   | Set the baudrate for device communication       |
| `:MPRepl`      | Open the integrated REPL                        |
| `:MPInit`      | Initialize a new project structure              |
| `:MPUpload`    | Upload the current file to the device           |
| `:MPUploadAll` | Upload the entire project with smart filtering  |
| `:MPEraseOne`  | Remove a file from the device                   |
| `:MPSetStubs`  | Configure board-specific stubs for autocomplete |

## Project Setup Workflow

1. Create a new project directory and optional virtual environment
2. Run `:MPInit` to generate the basic project structure
3. Configure your connection with `:MPSetPort` and `:MPSetBaud`
4. Select appropriate board stubs with `:MPSetStubs`
5. Install dependencies with `pip install -r requirements.txt`
6. Start developing with `:MPRun` to test your code

The initialization process creates several helpful files:

- A starter `main.py` example that blinks the onboard LED
- Configuration files for Ampy, type stubs, and linting
- A requirements.txt with necessary dependencies

## Smart Defaults

The plugin comes with intelligent defaults to make your workflow smoother:

- Automatic port and baud rate detection from existing .ampy files
- Smart file filtering during uploads (ignoring git files, caches, etc.)
- Board-specific stub configuration for improved code completion
- Sensible default delay settings for reliable device communication

## Development Status

Feature roadmap:

- ✅ Single file execution and upload
- ✅ Full project upload with filtering
- ✅ File deletion capabilities
- ✅ Project initialization and configuration
- ⏳ Bulk file deletion option
- ⏳ Retrieve files from device

## Acknowledgments

This project was inspired by [nvim-platformio.lua](https://github.com/anurag3301/nvim-platformio.lua) and aims to bring similar workflow improvements to the MicroPython ecosystem.

---

View the [full documentation](https://github.com/jim-at-jibba/micropython.nvim) on GitHub.
