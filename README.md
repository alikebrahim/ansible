# Pop!_OS Ansible Automation

This repository contains Ansible playbooks and roles for automating the setup and configuration of a Pop!_OS development workstation. It follows standard Ansible practices and includes a comprehensive set of roles for different aspects of system configuration.

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
│   ├── pop_os/               # Pop!_OS specific configuration
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

### Selective Execution

You can use tags to run specific parts of the playbook:

```bash
# Install only packages
ansible-playbook local.ansible.yml --tags "packages"

# Configure SSH settings
ansible-playbook local.ansible.yml --tags "ssh"

# Install development tools
ansible-playbook local.ansible.yml --tags "development"

# Skip certain tasks
ansible-playbook local.ansible.yml --skip-tags "ui"

# Run multiple tags
ansible-playbook local.ansible.yml --tags "shell,terminal"
```

## Tag Reference

The playbook uses a hierarchical tagging system for precise control:

### System Configuration
- `packages`: System package installation
- `apt_repositories`: System package repositories
- `security`: Security-related tasks
- `ssh`: SSH configuration
- `system`: General system configuration

### Development Environment
- `development`: All development-related tasks
- `languages`: Programming language setup
- `git_repositories`: Git repository management
- `node`: Node.js setup
- `build`: Build tools

### User Interface
- `ui`: UI-related tasks
- `fonts`: Font installation
- `terminal`: Terminal configuration

### Command Line
- `shell`: Shell configuration
- `zsh`: ZSH-specific configuration
- `documentation`: Documentation tools

### Applications
- `apps`: Application installation tasks
- `binaries`: Binary application installation
- `dotfiles`: Dotfiles management

### Special Tags
- `repositories`: All repository tasks (includes both `apt_repositories` and `git_repositories`)
- `always`: Tasks that always run

## Task Map

Below is a breakdown of which roles handle specific functionalities:

| Role          | Functionality                                       | Main Tags                       |
|---------------|----------------------------------------------------|---------------------------------|
| `pop_os`      | System repositories and package installation        | `apt_repositories`, `packages`  |
| `common`      | SSH, security, and basic system configuration       | `ssh`, `security`, `system`     |
| `development` | Languages, git repos, and development tools         | `languages`, `git_repositories` |
| `dotfiles`    | Dotfiles management with stow                       | `dotfiles`                      |
| `apps`        | Applications and binary installations               | `apps`, `binaries`              |
| `shell`       | ZSH configuration, shell utilities                  | `shell`, `zsh`                  |
| `terminal`    | Terminal emulator configuration                     | `terminal`                      |
| `fonts`       | Font installation and configuration                 | `fonts`, `ui`                   |

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