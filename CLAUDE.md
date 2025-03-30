# POP!_OS ANSIBLE AUTOMATION GUIDELINES

This Ansible playbook is specifically designed for Pop!_OS systems.

## COMMANDS
- Run playbook: `ansible-playbook local.ansible.yml`
- Run specific role: `ansible-playbook local.ansible.yml --tags "common"`
- Skip tasks: `ansible-playbook local.ansible.yml --skip-tags "packages"`
- Lint code: `ansible-lint local.ansible.yml`
- Run molecule tests: `cd roles/ROLE && molecule test`
- Test single role: `cd roles/ROLE && molecule converge -- --tags=ssh`

## STYLE GUIDELINES
- **YAML**: 2-space indentation, always use `---` at file start
- **Task naming**: Use descriptive task names, start with verb (Install, Configure, etc.)
- **Modules**: Use fully qualified module names (ansible.builtin.*)
- **Variables**: Use snake_case for variables, all lowercase
- **Tags**: Apply tags to all tasks for selective execution
- **Error handling**: Use ignore_errors, failed_when, and changed_when appropriately
- **Role organization**: Follow standard role structure (tasks/, vars/, meta/)
- **Conditionals**: Prefer when: over separate tasks with conditionals when possible
- **Comments**: Add comments for complex logic or unusual code

## BEST PRACTICES
- Check tasks with `--check` and `--diff` before applying to system
- Use molecule for role testing
- Use ansible-lint to enforce code quality