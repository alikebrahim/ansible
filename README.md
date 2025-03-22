# Personal Ansible Configuration

A comprehensive Ansible setup for managing personal workstation configurations across multiple Linux distributions (PopOS, Debian, Arch).

reference: https://opensource.com/article/18/3/manage-workstation-ansible

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
│   ├── dotfiles/      # Dotfiles configuration via stow
│   ├── fonts/         # Font installation
│   ├── shell/         # Shell configuration (zsh)
│   └── terminal/      # Terminal configuration
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
ansible-playbook local.ansible.yml
```

### Selective Execution

Run specific parts of the configuration using tags:

```bash
# Only setup fonts and terminal
ansible-playbook local.ansible.yml --tags "fonts,terminal"

# Only install programming languages
ansible-playbook local.ansible.yml --tags "languages"

# Only setup development tools
ansible-playbook local.ansible.yml --tags "go,rust,node"
```

### Dry Run

Test changes without actually applying them:

```bash
ansible-playbook local.ansible.yml --check
```

## Supported Distributions

- **Pop!_OS**: Primary development environment
- **Debian**: Secondary environment
- **Arch Linux**: Partially supported

## Customization

### Adding New Configuration

1. For distribution-specific configuration, add tasks to the respective directory under `system/`
2. For common configuration:
   - Create a new role under `roles/`
   - Add the role to `local.ansible.yml`

### Modifying Variables

Edit files in the `vars/` directory to customize:

- Package lists
- Dotfiles configuration
- Path settings

## Requirements

- Ansible 2.9+
- Sudo privileges on the target system

## SSH Keys and Ansible Vault

This repository uses Ansible Vault to encrypt SSH keys in the `.ssh/` directory.

### Encrypting SSH Keys

```bash
# Encrypt an SSH key file
ansible-vault encrypt ~/.ssh/id_rsa

# Encrypt multiple files
ansible-vault encrypt ~/.ssh/id_rsa ~/.ssh/id_rsa.pub
```

### Decrypting SSH Keys

```bash
# Decrypt an SSH key file
ansible-vault decrypt ~/.ssh/id_rsa

# Decrypt multiple files
ansible-vault decrypt ~/.ssh/id_rsa ~/.ssh/id_rsa.pub
```

### Using Encrypted Keys with Playbooks

When running playbooks that need access to encrypted SSH keys:

```bash
ansible-playbook local.ansible.yml --ask-vault-pass
```