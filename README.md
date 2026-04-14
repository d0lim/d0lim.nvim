# d0lim.nvim

A personal Neovim configuration based on [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) — a single-file, fully-documented starting point. This fork adds opinionated defaults and extra integrations (Kotlin LSP, neo-tree file explorer, etc.) while keeping the original single-`init.lua` layout.

## Features

**Core**
- [lazy.nvim](https://github.com/folke/lazy.nvim) — plugin manager, auto-bootstraps on first run
- [tokyonight](https://github.com/folke/tokyonight.nvim) — colorscheme
- [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter) (main branch) — syntax highlighting & indentation
- [mini.nvim](https://github.com/echasnovski/mini.nvim) — statusline, textobjects, surround

**Navigation / Search**
- [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim) + fzf-native — fuzzy finder (`<leader>s*`)
- [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) — left-side file tree, auto-opens on startup, auto-expands on focus
- [which-key.nvim](https://github.com/folke/which-key.nvim) — keybinding hints

**LSP / Completion / Formatting**
- [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) + [mason](https://github.com/mason-org/mason.nvim) + mason-lspconfig + mason-tool-installer
- JetBrains [kotlin-lsp](https://github.com/Kotlin/kotlin-lsp) integration (manual install, not via Mason)
- [conform.nvim](https://github.com/stevearc/conform.nvim) — format-on-save
- [blink.cmp](https://github.com/saghen/blink.cmp) + [LuaSnip](https://github.com/L3MON4D3/LuaSnip) — completion & snippets

**Git**
- [gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim) — gutter indicators, hunk actions

**Opt-in** (in `lua/kickstart/plugins/`, enable by uncommenting the `require` in `init.lua`)
- `debug` (nvim-dap), `lint` (nvim-lint), `autopairs`, `indent_line`

## Requirements

- **Neovim** 0.12.0+ (nightly) — required by the `nvim-treesitter` main branch
- **git**, **make**, **unzip**, C compiler (gcc/clang)
- [ripgrep](https://github.com/BurntSushi/ripgrep), [fd](https://github.com/sharkdp/fd)
- [**tree-sitter-cli**](https://github.com/tree-sitter/tree-sitter) `0.26.1`+
  - macOS: `brew install tree-sitter-cli`
  - Arch: `sudo pacman -S tree-sitter-cli`
  - Debian/Ubuntu/Fedora: `cargo install tree-sitter-cli` (or build from source)
  - Do **not** install via npm — nvim-treesitter's main branch does not support the npm build
  - Homebrew's `tree-sitter` formula is library-only; use `tree-sitter-cli` for the binary
- A [Nerd Font](https://www.nerdfonts.com/) (optional, for icons — set `vim.g.have_nerd_font = true` in `init.lua`)
- Clipboard tool: `pbcopy` on macOS, `xclip`/`xsel`/`wl-clipboard` on Linux, `win32yank` on Windows

### Language-specific

- **Kotlin**: install JetBrains' LSP — `brew install JetBrains/utils/kotlin-lsp`
- **TypeScript/JavaScript**: `npm`
- **Go**: `go`
- Others: Mason installs most LSPs automatically (`:Mason`)

## Install

Back up any existing configuration first:

```sh
mv ~/.config/nvim ~/.config/nvim.bak
mv ~/.local/share/nvim ~/.local/share/nvim.bak
```

Clone into the Neovim config directory:

```sh
git clone https://github.com/d0lim/d0lim.nvim.git ~/.config/nvim
```

Launch Neovim — lazy.nvim bootstraps itself and installs every plugin on first run:

```sh
nvim
```

Check installation with `:checkhealth`. View plugin status with `:Lazy`.

### Parallel install (keep alongside another config)

Use `NVIM_APPNAME` to run this config under a separate directory:

```sh
git clone https://github.com/d0lim/d0lim.nvim.git ~/.config/d0lim-nvim
alias nv-d0lim='NVIM_APPNAME=d0lim-nvim nvim'
```

## Keymaps (highlights)

Leader is `<space>`.

| Keys | Action |
|---|---|
| `<leader>sf` | Find files |
| `<leader>sg` | Live grep |
| `<leader>sh` | Search help |
| `<leader>sk` | Search keymaps |
| `<leader>e` | Toggle file explorer |
| `\` | Reveal current file in tree |
| `<C-h>` / `<C-l>` | Focus left/right window |
| `grd` | LSP: go to definition |
| `grr` | LSP: references |
| `gri` | LSP: implementation |
| `grn` | LSP: rename |
| `gra` | LSP: code action |
| `K` | Hover docs |
| `<C-o>` / `<C-i>` | Jump back / forward |

In neo-tree: `i` show file details, `H` toggle hidden, `<` / `>` resize width, `?` full help.

Press any prefix (e.g. `<leader>`, `g`, `<C-w>`) and wait — which-key shows what's available.

## Platform install recipes

<details><summary>macOS (Homebrew)</summary>

```sh
brew install neovim ripgrep fd tree-sitter-cli make
# for Kotlin:
brew install JetBrains/utils/kotlin-lsp
```

</details>

<details><summary>Ubuntu / Debian</summary>

```sh
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install make gcc ripgrep fd-find unzip git xclip neovim
cargo install tree-sitter-cli
```

</details>

<details><summary>Arch</summary>

```sh
sudo pacman -S --noconfirm --needed gcc make git ripgrep fd tree-sitter-cli unzip neovim
```

</details>

<details><summary>Fedora</summary>

```sh
sudo dnf install -y gcc make git ripgrep fd-find unzip neovim
cargo install tree-sitter-cli
```

</details>

## Credits

This configuration started from [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim). The kickstart documentation remains a good reference for understanding how `init.lua` is organized — it's heavily commented and meant to be read top to bottom.
