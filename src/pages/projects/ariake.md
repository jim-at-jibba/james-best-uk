---
layout: ../../layouts/ProjectLayout.astro
title: "Ariake.nvim :: Neovim Theme"
description: Ariake is a beautiful dark theme for Neovim.
tags: ["neovim", "theme", "open-source"]
githubUrl: https://github.com/jim-at-jibba/ariake.nvim
timestamp: 2024-02-24T02:39:03+00:00
featured: false
filename: ariake
---

# Ariake: An Elegant Dark Color Theme for Neovim

Ariake offers a sophisticated, visually appealing dark color palette designed to enhance your coding experience in Neovim. With carefully selected colors that reduce eye strain while providing optimal contrast for code readability, Ariake creates the perfect environment for long coding sessions.

## Installation

Getting started with Ariake is straightforward. The theme requires a Neovim plugin manager, with [Lazy.nvim](https://github.com/folke/lazy.nvim) being the recommended option.

### Installation with Lazy.nvim

Add the following to your Neovim configuration:

```lua
return {
    {
        'jim-at-jibba/ariake.nvim',
        config = function()
            vim.cmd.colorscheme 'ariake'
        end
    }
}
```

Once configured, restart Neovim or run `:Lazy sync` to apply the theme.

## Beyond Neovim

Ariake isn't limited to just your editor. Create a consistent visual experience across your development environment with additional themes for:

- [Kitty Terminal](https://sw.kovidgoyal.net/kitty/) - Bring the Ariake aesthetic to your terminal
- [Spacebar](https://github.com/cmacrae/spacebar) - Extend the theme to your macOS status bar

All additional themes can be found in the extras folder of the repository.

## Experience Ariake

Visit the [Ariake Repository](https://github.com/jim-at-jibba/ariake.nvim) to learn more and see screenshots showcasing the theme in action.
