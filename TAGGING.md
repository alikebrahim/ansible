# Ansible Tagging Convention Guide

This document provides detailed information about the tagging conventions used in this Ansible playbook. Tags allow for selective execution of tasks and roles, making it easier to run specific parts of the playbook.

## Tag Hierarchy

The playbook uses a hierarchical tagging system where:

1. **Role-level tags**: Represent entire roles (e.g., `common`, `development`)
2. **Functional tags**: Represent specific functionality (e.g., `ssh`, `packages`)
3. **Categorical tags**: Group related functionalities (e.g., `repositories` includes both `apt_repositories` and `git_repositories`)

## Tag Categories

### System Configuration
- **`packages`**: System package installation tasks
  - Used in: `system_packages/tasks/packages.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "packages"`

- **`apt_repositories`**: System package repository configuration
  - Used in: `system_packages/tasks/repositories.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "apt_repositories"`

- **`repositories`**: Parent tag for all repository-related tasks
  - Includes both `apt_repositories` and `git_repositories`
  - Example: `ansible-playbook local.ansible.yml --tags "repositories"`

- **`security`**: Security-related configurations
  - Used in: `common/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "security"`

- **`ssh`**: SSH key and configuration
  - Used in: `common/tasks/ssh.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "ssh"`

- **`system`**: General system-level configurations
  - Used in: `common/tasks/main.yml` 
  - Example: `ansible-playbook local.ansible.yml --tags "system"`

### Development Environment
- **`development`**: Development environment setup
  - Used in: `development/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "development"`

- **`languages`**: Programming language setup
  - Used in: `development/tasks/languages.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "languages"`

- **`git_repositories`**: Git repository cloning and management
  - Used in: `development/tasks/repositories.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "git_repositories"`

- **`node`**: Node.js and npm setup
  - Used in: `development/tasks/languages.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "node"`

- **`build`**: Build tools and compilation dependencies
  - Used in: `development/tasks/build.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "build"`

- **`github`**: GitHub CLI and configuration
  - Used in: `development/tasks/github.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "github"`

### User Interface
- **`ui`**: UI-related configurations and applications
  - Used in: `apps/tasks/main.yml`, `fonts/tasks/main.yml`, `terminal/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "ui"`

- **`fonts`**: Font installation and configuration
  - Used in: `fonts/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "fonts"`

- **`terminal`**: Terminal emulator configuration
  - Used in: `terminal/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "terminal"`

### Command Line
- **`shell`**: Shell configuration and tools
  - Used in: `shell/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "shell"`

- **`zsh`**: ZSH-specific configuration
  - Used in: `shell/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "zsh"`

- **`documentation`**: Documentation-related tools
  - Used in: `shell/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "documentation"`

### Applications
- **`apps`**: Application installation
  - Used in: `apps/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "apps"`

- **`binaries`**: Binary application installation
  - Used in: `apps/tasks/binaries.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "binaries"`

- **`dotfiles`**: Dotfiles management with stow
  - Used in: `dotfiles/tasks/main.yml`
  - Example: `ansible-playbook local.ansible.yml --tags "dotfiles"`

### Special Tags
- **`always`**: Tasks that always run regardless of specified tags
  - Used for critical tasks like PackageKit management
  - These tasks run even when using `--tags` with other tags

## Tag Combinations

Tags can be combined to run specific combinations of tasks:

```bash
# Install packages and configure SSH
ansible-playbook local.ansible.yml --tags "packages,ssh"

# Set up complete development environment
ansible-playbook local.ansible.yml --tags "development,languages,git_repositories"

# Configure all UI components
ansible-playbook local.ansible.yml --tags "ui"

# Install applications but skip UI components
ansible-playbook local.ansible.yml --tags "apps,binaries" --skip-tags "ui"
```

## Tag Inheritance

Tasks included from other files inherit the tags of the include task. For example:

```yaml
- name: Include repositories tasks
  ansible.builtin.include_tasks: repositories.yml
  tags: [repositories, git_repositories]
```

This means all tasks in `repositories.yml` will have both the `repositories` and `git_repositories` tags.

## Best Practices for Tags

1. **Be specific**: Apply the most specific tag to each task
2. **Use hierarchical tagging**: Apply both specific and general tags where appropriate
3. **Be consistent**: Use the same tag for similar functionality across different roles
4. **Test tags**: Verify tag behavior with `ansible-playbook --list-tasks --tags "tag_name"`
5. **Document tags**: Keep this documentation updated when adding new tags

## Adding New Tags

When adding new tags:

1. Make sure they follow the existing hierarchical structure
2. Update this documentation to include the new tag
3. Test the tag with `--list-tasks` to ensure it selects the intended tasks
4. Consider backward compatibility with existing tag usage