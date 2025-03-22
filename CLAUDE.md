# Ansible Configuration Guidelines

## Commands
- Run playbook: `ansible-playbook local.ansible.yml`
- Run specific tasks: `ansible-playbook local.ansible.yml --tags "go,rust,node"`
- Check mode (dry run): `ansible-playbook local.ansible.yml --check`
- Syntax check: `ansible-playbook --syntax-check local.ansible.yml`
- Lint: `ansible-lint local.ansible.yml`

## Style Guidelines
- **Task naming**: Use clear, descriptive names starting with a verb
- **Indentation**: Two spaces for all YAML files
- **Variables**: Use snake_case for variable names
- **Path handling**: Use `{{ lookup('env', 'HOME') }}` for home directory
- **Tags**: Add tags to tasks for selective execution
- **Comments**: Document non-obvious tasks or conditional logic
- **Task files**: Organize by function (core, apps, languages)
- **Distribution-specific**: Use separate directories for different OS distributions
- **Error handling**: Use `ignore_errors` sparingly, prefer `failed_when`

## Repository Organization
- System-specific configurations in system/ directory
- Group tasks by function rather than distribution
- Use fully qualified module names (ansible.builtin.*)