---
layout: ../../layouts/ProjectLayout.astro
title: "Micropython.nvim :: Neovim Plugin"
description: A Neovim plugin for working with Micropython projects.
tags: ["lua", "neovim", "micropython", "tool"]
githubUrl: https://github.com/jim-at-jibba/micropython.nvim
timestamp: 2024-03-19T02:39:03+00:00
featured: false
filename: micropython
---

# micropython_nvim

## Streamlined MicroPython Development Inside Neovim

micropython_nvim is a Neovim plugin I created to enhance the MicroPython development experience. It brings the convenience of modern development workflows to microcontroller programming, allowing you to run code, manage files on the device, flash firmware and use the REPL without ever leaving your editor.

Version 3 is a ground-up rework built on [mpremote](https://docs.micropython.org/en/latest/reference/mpremote.html), the official MicroPython remote control tool, and it now has its own [documentation site](https://micropython-nvim.jamesbest.uk).

### Key Features

- **Run**: Run local Python files on your microcontroller without uploading them
- **Upload**: Upload files to the device, keeping the project's folders, or on every save
- **Mount**: Mount your local directory on the device for live development without uploading
- **REPL**: A persistent split where you can send the current line, a selection or the whole buffer, and stop running code
- **File Browser**: Browse, edit, delete, download and create files and folders on the device
- **Device Management**: List connected devices, reset, show device info and set its clock
- **Packages**: Install micropython-lib and GitHub packages on the device with `mip`
- **Firmware**: Install or update MicroPython on the board with [mpflash](https://github.com/Josverl/mpflash)
- **Project Initialization**: Type stubs matched to the connected board, set up for pyright
- **Statusline Integration**: See your connection status at a glance

## Getting Started

### Prerequisites

- Neovim 0.9 or higher
- [mpremote](https://docs.micropython.org/en/latest/reference/mpremote.html)
- [uv](https://docs.astral.sh/uv/) for dependency management (Unix-only)
- [snacks.nvim](https://github.com/folke/snacks.nvim) (optional, for nicer terminals and pickers)
- [mpflash](https://github.com/Josverl/mpflash) (optional, for flashing firmware)

### Installation

Using lazy.nvim:

```lua
{
    "jim-at-jibba/micropython.nvim",
    dependencies = { "folke/snacks.nvim" }, -- optional
    config = function()
        require("micropython_nvim").setup()
    end,
}
```

Call `setup()` even if you don't change any options, as it reads the project's `.micropython` file when Neovim starts. Run `:checkhealth micropython_nvim` (or `:MP health`) to check your setup.

### Basic Configuration

Add a keybinding to run your code:

```lua
vim.keymap.set("n", "<leader>mr", require("micropython_nvim").run, { desc = "MicroPython: run file" })
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

Everything lives under a single `:MP` command. Type `:MP <Tab>` to see the subcommands, or run `:MP` on its own to pick one from a list.

| Command            | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `:MP run`          | Run the current file on the device without uploading it  |
| `:MP run_main`     | Run the project's `main.py` from any buffer              |
| `:MP upload`       | Upload the current file, keeping its project path        |
| `:MP upload_all`   | Upload the whole project, skipping unchanged files       |
| `:MP mount`        | Mount the project on the device without copying anything |
| `:MP repl`         | Open or focus the REPL split                             |
| `:MP send`         | Send the current line, or a range of lines, to the REPL  |
| `:MP interrupt`    | Interrupt code running in the REPL                       |
| `:MP files`        | Browse, open, edit, download and delete device files     |
| `:MP erase`        | Erase one file or folder on the device                   |
| `:MP info`         | Show the firmware, board, storage and clock              |
| `:MP mip`          | Install a package on the device with mip                 |
| `:MP flash`        | Install or update MicroPython firmware with mpflash      |
| `:MP init`         | Create a new project with stubs for the connected device |
| `:MP set_stubs`    | Switch the project to different stubs                    |
| `:MP set_port`     | Choose the port the device is on                         |

The [commands reference](https://micropython-nvim.jamesbest.uk/commands/) covers the full list.

## Project Setup Workflow

1. Plug in your device, create a project directory and open Neovim in it
2. Run `:MP init`, which detects the connected board and suggests matching type stubs
3. Answer yes to `uv sync` to install the project's dependencies
4. Open `main.py` and run `:MP run` to test your code

The initialization process creates several helpful files:

- A starter `main.py` example that blinks the onboard LED
- A `pyproject.toml` with the project's dependencies
- A `.micropython` file holding the project's device settings
- A `pyrightconfig.json` set up for the board's type stubs

## Smart Defaults

The plugin comes with sensible defaults to make your workflow smoother:

- Board detection and automatic stubs for improved code completion
- Uploads keep your project's folder structure and skip unchanged files
- Development-only files like `typings/` and `pyrightconfig.json` are never uploaded
- Confirmation before erasing anything on the device
- The REPL holds the port while it's open, so `:MP run` sends your code to the open REPL instead of fighting it for the connection

## Upgrading from v2

v3 puts every command under `:MP`, so `:MPRun` becomes `:MP run` and so on. It also replaces `.ampy` files with `.micropython`, drops the baud rate setting, and no longer needs toggleterm.nvim or dressing.nvim. The [migration guide](https://micropython-nvim.jamesbest.uk/migrating-from-v2/) lists every breaking change and what to do about it.

## Acknowledgments

This project was inspired by [nvim-platformio.lua](https://github.com/anurag3301/nvim-platformio.lua) and aims to bring similar workflow improvements to the MicroPython ecosystem.

---

View the [full documentation](https://micropython-nvim.jamesbest.uk) or the [source on GitHub](https://github.com/jim-at-jibba/micropython.nvim).
