# Ansible Playbook Task Execution Flow

This document outlines the sequential order of tasks that run when executing the local.ansible.yml playbook.

## Repository Cloning Play

1. Ensure project directories exist
2. Clone development tool repositories
   - Neovim
   - Tmux
   - Btop
   - Fzf

## System Environment Play

### Pre-tasks
1. Stop PackageKit service
2. Install required Ansible collections (community.general)

### System Packages Role
1. Add various package repositories (Docker, Wezterm, GitHub CLI, 1Password)
2. Update apt cache
3. Install core packages (curl, git, stow, jq, etc.)
4. Install development packages (make, gcc, python3-dev, etc.)
5. Install tool packages (wezterm, neofetch, gh, etc.)

### Common Role
1. Check if Tailscale is installed
2. Install Tailscale if not present
3. Configure sudoers with template

### System Tasks
1. Get latest Go version and install Go
2. Compile & install Neovim (from cloned source)
3. Compile & install Tmux (from cloned source)
4. Compile & install Btop (from cloned source)

### Post-tasks
1. Start PackageKit service

## User Environment Play

### Development Role (User)
1. Install user-level languages (nvm, node, rust via rustup)
2. Build user-level applications (fzf)
3. Configure GitHub settings

### Dotfiles Role
1. Clone dotfiles repository
2. Apply dotfiles using stow

### Apps Role
1. Create apps directory
2. Install browser applications
3. Install binary applications (Obsidian, Logseq)

### Shell Role
1. Set zsh as default shell
2. Update tldr database
3. Install and configure atuin (shell history)

### Terminal Role
1. Configure wezterm as default terminal

### Fonts Role
1. Install JuliaMono and JetBrains Mono fonts
2. Update font cache