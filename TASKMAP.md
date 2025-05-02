# Ansible Playbook Task Map

This document provides a visual map of tasks in this Ansible playbook, showing the relationships between roles, tasks, and tags.

## Playbook Structure

```
local.ansible.yml
├── COMMON SETUP
│   └── PackageKit Service Management [always]
│
├── ROLE: system_packages
│   ├── repositories.yml [apt_repositories, repositories]
│   │   ├── Create apt keyrings directory
│   │   ├── Add apt repository keys
│   │   └── Configure apt repositories
│   │
│   └── packages.yml [packages]
│       ├── Update apt cache
│       └── Install packages
│
├── ROLE: common
│   ├── ssh.yml [ssh, security]
│   │   ├── Install SSH keys
│   │   └── Configure SSH settings
│   │
│   └── main.yml [system, security]
│       ├── Install Tailscale [system]
│       └── Configure sudoers [security]
│
├── ROLE: development
│   ├── languages.yml [languages]
│   │   ├── Setup Node.js [node, languages]
│   │   ├── Setup Python environments [languages]
│   │   └── Setup Go [languages]
│   │
│   ├── repositories.yml [git_repositories, repositories]
│   │   └── Clone development tool repositories
│   │
│   ├── build.yml [build]
│   │   └── Install build dependencies
│   │
│   └── github.yml [github, development]
│       └── Configure GitHub CLI
│
├── ROLE: dotfiles
│   └── main.yml [dotfiles]
│       ├── Install stow [dotfiles, packages]
│       ├── Clone dotfiles repository
│       └── Apply dotfiles with stow
│
├── ROLE: apps
│   ├── main.yml [apps]
│   │   ├── Create apps directory
│   │   └── Install UI applications [ui]
│   │
│   └── binaries.yml [binaries, apps]
│       └── Install binary applications
│
├── ROLE: shell
│   └── main.yml [shell]
│       ├── Configure ZSH [shell, zsh]
│       ├── Install documentation tools [documentation, shell]
│       └── Install shell utilities (atuin, etc.)
│
├── ROLE: terminal
│   └── main.yml [terminal, ui]
│       ├── Install terminal emulator
│       └── Configure terminal settings
│
└── ROLE: fonts
    └── main.yml [fonts, ui]
        ├── Create font directories
        ├── Install fonts
        └── Update font cache
```

## Task Execution Flow

The playbook follows this general execution flow:

1. Initial setup (PackageKit service stop)
2. System repositories (system_packages role)
3. System packages (system_packages role)
4. System configuration (common role)
5. Development environment (development role)
6. Application installation (apps role)
7. User configuration (dotfiles, shell, terminal roles)
8. UI configuration (fonts role)
9. Final cleanup (PackageKit service start)

## Critical Path Dependencies

Some tasks depend on others to function properly:

- Package installation depends on repository configuration
- Dotfiles application depends on stow installation
- Development tools may depend on build dependencies
- Terminal configuration depends on terminal emulator installation

## Common Execution Patterns

Here are some common tag combinations for specific scenarios:

### Initial System Setup
```bash
ansible-playbook local.ansible.yml --tags "apt_repositories,packages,security,system"
```

### Development Environment Setup
```bash
ansible-playbook local.ansible.yml --tags "development,languages,git_repositories,build,github"
```

### User Environment Configuration
```bash
ansible-playbook local.ansible.yml --tags "dotfiles,shell,terminal,fonts,ui"
```

### Application Installation
```bash
ansible-playbook local.ansible.yml --tags "apps,binaries"
```

### Security Configuration
```bash
ansible-playbook local.ansible.yml --tags "security,ssh"
```

## Adding New Tasks

When adding new tasks to the playbook:

1. Identify the appropriate role based on functionality
2. Add the task to the correct task file within that role
3. Apply appropriate tags following the tagging convention
4. Update this task map if adding significant new functionality