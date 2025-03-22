# Personal Ansible Configuration

A comprehensive Ansible setup for managing personal workstation configurations across Linux distributions (PopOS, Debian, Arch).

## Overview

This repository contains Ansible playbooks and roles to automate the setup and configuration of development workstations. It handles:

- Package installation (via apt, cargo, go)
- Development environment setup (programming languages, tools)
- Terminal and shell configuration (zsh, wezterm)
- Dotfiles management (via stow)
- Font installation
- System configuration

## Structure

```
ansible/
├── files/             # Static files for playbooks
├── local.ansible.yml  # Main playbook
├── roles/             # Reusable configuration components
├── system/            # Distribution-specific tasks
│   ├── archlinux/     # Arch Linux specific configuration
│   ├── debian/        # Debian specific configuration
│   └── popOS/         # Pop!_OS specific configuration
└── vars/              # Variable files for different distributions
```

## Usage

### Basic Execution

Run the entire playbook to set up your system:

```bash
ansible-playbook local.ansible.yml --ask-become-pass --ask-vault-pass
```

### Selective Execution

Run specific parts of the configuration using tags:

```bash
# Only setup fonts and terminal
ansible-playbook local.ansible.yml --ask-become-pass --tags "fonts,terminal"

# Only install programming languages
ansible-playbook local.ansible.yml --ask-become-pass --tags "languages"

# Only setup development tools
ansible-playbook local.ansible.yml --ask-become-pass --tags "go,rust,node"
```

### Dry Run

Test changes without actually applying them:

```bash
ansible-playbook local.ansible.yml --ask-become-pass --check
```

## Supported Distributions

- **Pop!_OS**: Primary development environment
- **Debian**: Secondary environment
- **Arch Linux**: Partially supported

## Customization

- For distribution-specific configuration, add tasks to the respective directory under `system/`
- For common configuration, create a new role under `roles/`
- Edit files in the `vars/` directory to customize package lists and configurations

## Requirements

- Ansible 2.9+
- Sudo privileges on the target system
