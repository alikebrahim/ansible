# Ubuntu/Pop!_OS Ansible Automation

This repository contains Ansible playbooks and roles for automating the setup and configuration of an Ubuntu or Pop!_OS development workstation. It follows standard Ansible practices and includes a comprehensive set of roles for different aspects of system configuration.

## Overview

These playbooks are designed to:

1. Install and configure system repositories
2. Install common development packages
3. Set up development environments for various languages
4. Configure SSH and security settings
5. Install command-line tools and applications
6. Configure shell, terminal, and UI preferences
7. Manage dotfiles
8. Install fonts and UI components

## Architecture

The playbook is structured with a **two-play architecture** that separates system-level and user-level tasks:

1. **System Play** - Runs with `become: true` to handle system-wide operations:
   - Package repository configuration
   - System package installation
   - System-level configuration
   - Operations requiring root privileges

2. **User Play** - Runs with `become: false` to configure user environment:
   - User dotfiles and configurations
   - User-specific application installations
   - Shell and terminal preferences
   - Programming language user environments
   - Home directory operations

This separation ensures proper privilege handling, maintains security best practices, and prevents unintended system-wide changes.

## Directory Structure

The playbook follows standard Ansible practices with the following structure:

```
ansible/
├── ansible.cfg               # Ansible configuration
├── files/                    # Static files for copying
│   ├── ssh/                  # SSH keys
│   └── sudoers_ansible       # Sudoers configuration
├── group_vars/               # Variables for all hosts
│   └── all.yml               # Common variables
├── hosts                     # Inventory file
├── local.ansible.yml         # Main playbook
├── requirements.yml          # Required collections
├── roles/                    # Role definitions
│   ├── apps/                 # Application installation
│   ├── common/               # Common system configuration
│   ├── development/          # Development tools and languages
│   ├── dotfiles/             # Dotfiles management
│   ├── fonts/                # Font installation
│   ├── system_packages/      # System packages and repositories configuration
│   ├── shell/                # Shell configuration
│   └── terminal/             # Terminal configuration
└── templates/                # Jinja2 templates
    └── sudoers_ansible.j2    # Sudoers template
```

## Usage

### Basic Usage

```bash
# Run the entire playbook
ansible-playbook local.ansible.yml

# Run with check mode (dry run)
ansible-playbook local.ansible.yml --check

# Run with diff to see changes
ansible-playbook local.ansible.yml --diff
```

### Context-Specific Execution

You can target specific execution contexts:

```bash
# Run only system-level tasks
ansible-playbook local.ansible.yml --tags "system"

# Run only user-level tasks
ansible-playbook local.ansible.yml --tags "user"
```

### Selective Execution

You can use tags to run specific parts of the playbook:

```bash
# Install only packages
ansible-playbook local.ansible.yml --tags "packages"

# Configure SSH settings
ansible-playbook local.ansible.yml --tags "ssh"

# Install development tools in system context
ansible-playbook local.ansible.yml --tags "development,system"

# Install development tools in user context
ansible-playbook local.ansible.yml --tags "development,user"

# Skip certain tasks
ansible-playbook local.ansible.yml --skip-tags "ui"

# Run multiple roles
ansible-playbook local.ansible.yml --tags "shell,terminal"
```

## Tag Reference

The playbook uses a hierarchical tagging system for precise control with context-aware tags:

### Context Tags
These tags determine which play/context the task runs in:
- `system`: Tasks that run in the system play with `become: true`
- `user`: Tasks that run in the user play with `become: false`

### Functional Tags
- `packages`: System package installation
- `apt_repositories`: System package repositories
- `security`: Security-related tasks
- `ssh`: SSH configuration
- `development`: All development-related tasks 
- `languages`: Programming language setup
- `git_repositories`: Git repository management
- `node`: Node.js setup
- `build`: Build tools
- `ui`: UI-related tasks
- `fonts`: Font installation
- `terminal`: Terminal configuration
- `shell`: Shell configuration
- `zsh`: ZSH-specific configuration
- `documentation`: Documentation tools
- `apps`: Application installation tasks
- `binaries`: Binary application installation
- `dotfiles`: Dotfiles management

### Special Tags
- `repositories`: All repository tasks (includes both `apt_repositories` and `git_repositories`)
- `always`: Tasks that always run
- `common`: Common system configuration tasks

## Role Context Map

Below is a breakdown of which roles operate in which context:

| Role              | System Context                                  | User Context                                  |
|-------------------|------------------------------------------------|----------------------------------------------|
| `system_packages` | Repository setup, package installation          | N/A (system-only role)                        |
| `common`          | Sudoers config, Tailscale installation         | SSH configuration                            |
| `development`     | Go system installation, build tool installation | Language user setup, repositories, Go packages |
| `dotfiles`        | N/A (user-only role)                           | Dotfiles management with stow                 |
| `apps`            | N/A (user-only role)                           | User binary and application installation      |
| `shell`           | N/A (user-only role)                           | ZSH configuration, shell utilities            |
| `terminal`        | N/A (user-only role)                           | Terminal emulator configuration               |
| `fonts`           | N/A (user-only role)                           | Font installation in user directory           |

## Development and Testing

### Linting

```bash
ansible-lint local.ansible.yml
```

### Testing with Molecule

```bash
# Test a specific role
cd roles/common && molecule test

# Run only the converge step
cd roles/common && molecule converge

# Test specific tags
cd roles/common && molecule converge -- --tags=ssh
```

## Best Practices

This playbook follows these best practices:

1. **Idempotent tasks**: Tasks are designed to be run multiple times without causing changes if already in the desired state
2. **Explicit error handling**: Uses `changed_when`, `failed_when`, and `ignore_errors` appropriately
3. **Consistent tagging**: Hierarchical tag system for selective execution
4. **Standard role structure**: Follows Ansible conventions for role organization
5. **Fully qualified module names**: Uses `ansible.builtin.*` naming for clarity
6. **Clear task naming**: Descriptive task names that start with verbs

## License

This project is licensed under the MIT License - see the LICENSE file for details.