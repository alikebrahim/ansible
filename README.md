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
├── group_vars/        # Centralized variables for all hosts
│   ├── all.yml        # Common variables across distributions
│   ├── debian.yml     # Debian-specific variables
│   └── popos.yml      # Pop!_OS-specific variables
├── local.ansible.yml  # Main playbook
├── roles/             # Reusable configuration components
│   ├── apps/          # AppImages and binary applications
│   ├── common/        # Common system configuration
│   ├── development/   # Development tools
│   ├── dotfiles/      # Dotfiles management with stow
│   ├── fonts/         # Font installation and configuration
│   ├── shell/         # Shell customization
│   └── terminal/      # Terminal emulator setup
├── tasks/             # Distribution-specific tasks
│   ├── debian/        # Debian-specific tasks
│   └── pop_os/        # Pop!_OS-specific tasks
├── templates/         # Jinja2 templates for configuration files
└── vault/             # Encrypted sensitive data
```

## Usage

### Basic Execution

Run the entire playbook to set up your system:

```bash
ansible-playbook local.ansible.yml --ask-become-pass
```

### Selective Execution

Run specific parts of the configuration using tags:

```bash
# Only setup fonts and terminal
ansible-playbook local.ansible.yml --ask-become-pass --tags "fonts,terminal"

# Only install programming languages
ansible-playbook local.ansible.yml --ask-become-pass --tags "languages"

# Only setup development tools
ansible-playbook local.ansible.yml --ask-become-pass --tags "packages,repositories"
```

### Dry Run

Test changes without actually applying them:

```bash
ansible-playbook local.ansible.yml --ask-become-pass --check
```

### Using Ansible Vault

Sensitive information can be securely stored using Ansible Vault:

```bash
# Encrypt the vault file
ansible-vault encrypt vault/secrets.yml

# Run playbook with encrypted vault
ansible-playbook local.ansible.yml --ask-vault-pass --ask-become-pass

# Edit encrypted vault
ansible-vault edit vault/secrets.yml
```

For convenience, you can store the vault password in a file:

```bash
# Create a password file (add to .gitignore)
echo "your-secure-password" > .vault_pass
chmod 600 .vault_pass

# Use password file with playbook
ansible-playbook local.ansible.yml --vault-password-file .vault_pass --ask-become-pass
```

## Tags Reference

The playbook uses the following tags for selective execution:

- `system`: Base system configuration
- `packages`: Package installation tasks
- `repositories`: Repository management
- `languages`: Programming language setup
- `ui`: User interface components
- `dotfiles`: Dotfiles management
- `security`: Security-related configuration
- `build`: Compilation tasks
- `shell`: Shell customization
- `terminal`: Terminal emulator setup
- `documentation`: Documentation tools

## Supported Distributions

- **Pop!_OS**: Primary development environment
- **Debian**: Secondary environment
- **Arch Linux**: Partially supported

## Customization

- For distribution-specific configuration, add tasks to the respective directory under `tasks/`
- For common configuration, create a new role under `roles/`
- Edit files in the `group_vars/` directory to customize package lists and configurations

## Requirements

- Ansible 2.9+
- Sudo privileges on the target system
- Community.general collection (installed automatically)

## Development

### Testing

The repository includes Molecule tests for roles. To run tests:

```bash
# Install dependencies
pip install molecule molecule-docker

# Test a specific role
cd roles/common
molecule test
```

### Linting

Ansible Lint is configured to check for common issues:

```bash
# Install dependencies
pip install ansible-lint

# Run linting
ansible-lint
```
