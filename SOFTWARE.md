# Software Installation Catalog

This document provides a comprehensive list of all software installed by this Ansible configuration, organized by category and installation method.

## Package Managers & Languages

### Cargo (Rust)
- **File**: `/roles/development/tasks/languages.yml`
- **Installation Method**: `rustup.sh`
- **URL**: `https://sh.rustup.rs`
- **Command**: `sh /tmp/rustup.sh -y`
- **Packages**:
  - ripgrep (primary installation method)
  - fd-find (primary installation method)
  - eza
  - zoxide
  - tokei
  - bat
  - git-delta

### Go
- **File**: `/roles/development/tasks/languages.yml`
- **Installation Method**: tarball download
- **URL**: `https://go.dev/dl/{{ go_version.stdout }}.linux-amd64.tar.gz`
- **Command**: `ansible.builtin.unarchive`
- **Packages**:
  - github.com/air-verse/air@latest
  - github.com/jesseduffield/lazygit@latest
  - github.com/go-delve/delve/cmd/dlv@latest

### Node.js (NVM)
- **File**: `/roles/development/tasks/languages.yml`
- **Installation Method**: shell script
- **URL**: `https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh`
- **Command**: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash`
- **Packages**:
  - @anthropic-ai/claude-code

### Python
- **File**: `/roles/development/tasks/languages.yml`
- **Installation Method**: shell script (pyenv and uv)
- **URLs**:
  - `https://pyenv.run`
  - `https://astral.sh/uv/install.sh`
- **Commands**:
  - `curl https://pyenv.run | bash`
  - `curl -LsSf https://astral.sh/uv/install.sh | sh`

## System Tools

### Shell Utilities
- **File**: `/roles/shell/tasks/main.yml`
- **Installation Method**: APT and shell script
- **Tools**:
  - zsh (APT)
  - tldr (APT)
  - atuin
    - **URL**: `https://setup.atuin.sh`
    - **Command**: `curl --proto '=https' --tlsv1.2 -LsSf https://setup.atuin.sh | sh`

### Network & VPN
- **File**: `/roles/common/tasks/main.yml`
- **Installation Method**: Shell script
- **Tools**:
  - Tailscale
    - **URL**: `https://tailscale.com/install.sh`
    - **Command**: `curl -fsSL https://tailscale.com/install.sh | sh`

### Security
- **File**: `/roles/common/tasks/main.yml`
- **Installation Method**: APT repository
- **Tools**:
  - 1Password CLI
    - **URL**: `https://downloads.1password.com/linux/keys/1password.asc`
    - **Repository**: `deb [arch={{ ansible_architecture }} signed-by=/usr/share/keyrings/1password-archive-keyring.gpg] https://downloads.1password.com/linux/debian/{{ ansible_architecture }} stable main`

## Development Tools

### Version Control
- **File**: `/roles/development/tasks/main.yml`
- **Installation Method**: APT repository
- **Tools**:
  - GitHub CLI (gh)
    - **URL**: `https://cli.github.com/packages/githubcli-archive-keyring.gpg`
    - **Repository**: `deb [arch={{ ansible_architecture }} signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main`

### Editors & IDEs

#### Neovim
- **File**: `/roles/development/tasks/build.yml`
- **Installation Method**: Git clone + build
- **URL**: `https://github.com/neovim/neovim`
- **Build Commands**:
  ```
  make CMAKE_BUILD_TYPE=RelWithDebInfo && make install
  ```

#### Helix
- **File**: `/roles/apps/tasks/main.yml`
- **Installation Method**: AppImage download
- **URL**: `https://github.com/helix-editor/helix/releases/download/24.02/helix-24.02-x86_64.AppImage`
- **Dest**: `{{ apps_dir }}/helix`

### Terminal Multiplexers

#### Tmux
- **File**: `/roles/development/tasks/build.yml`
- **Installation Method**: Git clone + build (not installed with APT)
- **URL**: `https://github.com/tmux/tmux.git`
- **Build Commands**:
  ```
  sh autogen.sh && ./configure && make && make install
  ```

#### Wezterm
- **File**: `/roles/apps/tasks/main.yml`
- **Installation Method**: AppImage download
- **URL**: `https://github.com/wez/wezterm/releases/download/20240326-113614-bbcac864/wezterm-20240326-113614-bbcac864-Ubuntu22.04.AppImage`
- **Dest**: `{{ apps_dir }}/wezterm`

### System Monitoring
- **File**: `/roles/development/tasks/build.yml`
- **Installation Method**: Git clone + build
- **Tools**:
  - btop
    - **URL**: `https://github.com/aristocratos/btop.git`
    - **Build Commands**: `make ADDFLAGS=-march=native && make install`

### Command Line Utilities
- **File**: `/roles/development/tasks/repositories.yml` and `/roles/development/tasks/build.yml`
- **Installation Method**: Git clone
- **Tools**:
  - fzf
    - **URL**: `https://github.com/junegunn/fzf.git`
    - **Install Command**: `~/.local/src/fzf/install --bin`

## Desktop Applications

### Note Taking
- **File**: `/roles/apps/tasks/main.yml`
- **Installation Method**: AppImage download
- **Tools**:
  - Obsidian
    - **URL**: `https://github.com/obsidianmd/obsidian-releases/releases/download/v1.8.9/Obsidian-1.8.9.AppImage`
    - **Dest**: `{{ apps_dir }}/obsidian`
  - Logseq
    - **URL**: `https://github.com/logseq/logseq/releases/download/0.10.9/Logseq-linux-x64-0.10.9.AppImage`
    - **Dest**: `{{ apps_dir }}/logseq`

### Security
- **File**: `/roles/apps/tasks/main.yml`
- **Installation Method**: Debian package
- **Tools**:
  - 1Password Desktop
    - **URL**: `https://downloads.1password.com/linux/debian/amd64/stable/1password-latest.deb`

## Fonts
- **File**: `/roles/fonts/tasks/main.yml`
- **Installation Method**: Archive download
- **Fonts**:
  - JuliaMono
    - **URL**: `https://github.com/cormullion/juliamono/releases/download/v0.056/JuliaMono-ttf.tar.gz`
  - JetBrains Mono
    - **URL**: `https://download.jetbrains.com/fonts/JetBrainsMono-2.304.zip`

## Configuration Management

### Dotfiles
- **File**: `/roles/dotfiles/tasks/main.yml`
- **Installation Method**: Git clone + stow
- **URL**: `{{ dotfiles_repo }}` (https://github.com/alikebrahim/dotfiles.git)
- **Command**: `stow -v {{ item }}` for each package in dotfiles_packages

## Distribution-Specific Packages

### Debian/Pop!_OS Core Packages
- **File**: `/tasks/debian/apt.yml` and `/tasks/pop_os/apt.yml`
- **Installation Method**: APT
- **Core Packages**:
  - curl
  - git
  - stow
  - jq
  - unzip
  - wget
  - zsh
  - htop
  - build-essential
  - ninja-build
  - gettext
  - libtool
  - libtool-bin
  - autoconf
  - automake
  - cmake
  - g++
  - pkg-config

### Development Packages
- **File**: `/tasks/debian/apt.yml` and `/tasks/pop_os/apt.yml`
- **Installation Method**: APT
- **Packages**:
  - libevent-dev
  - ncurses-dev
  - bison
  - python3-dev
  - python3-pip
  - gcc
  - make
  - libfuse2
  - libssl-dev

### Tool Packages
- **File**: `/tasks/debian/apt.yml` and `/tasks/pop_os/apt.yml`
- **Installation Method**: APT
- **Packages**:
  - tldr
  - neofetch
  - fzf