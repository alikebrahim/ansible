# Ansible Playbook Refactor Plan: Best Practices & System Safety

## Overview
This document provides a comprehensive plan to restructure the `alikebrahim-ansible` playbook to follow Ansible best practices for personal workstation automation. The primary goals are:

1. **Prevent system-wide unintended consequences** (e.g., root-owned files in `$HOME`).
2. **Ensure user-specific configuration runs with minimal privileges.**
3. **Maintain clarity, idempotency, and easy debugging.**
4. **Provide clean separation of concerns** between system-level and user-level configuration.

We will adopt the **two-play structure** pattern, unless noted otherwise with justified rationale.

---

## Refactor Strategy Summary
- **Split the playbook into two distinct plays**:
  1. **User-scope Play:** No privilege escalation (`become: false`)
  2. **System-scope Play:** Elevated privileges for necessary tasks (`become: true`)
- **Update roles and tasks** to explicitly handle user/system concerns.
- **Refactor variables** to clearly distinguish between `ansible_user_id` and the real user.
- **Audit and correct all tasks affecting `$HOME`** to run without elevated privileges.

---

## Step-by-Step Refactor Plan

### 1. Restructure `local.ansible.yml` into Two Plays

#### **Before**:
```yaml
- name: Configure Personal Workstation
  hosts: localhost
  connection: local
  become: true
  roles:
    - pop_os
    - common
    - development
    - dotfiles
    - apps
    - shell
    - terminal
    - fonts
```

#### **After**:
```yaml
- name: Configure User Environment
  hosts: localhost
  connection: local
  become: false
  vars:
    real_user: alikebrahim
  roles:
    - dotfiles
    - apps
    - shell
    - terminal
    - fonts
    - development   # user-level tasks only

- name: Configure System Environment
  hosts: localhost
  connection: local
  become: true
  roles:
    - pop_os
    - common
    - development   # system-level tasks only
```

### 2. Update Variable Usage for User Identification

- **Create `group_vars/all.yml` Update:**
  ```yaml
  real_user: alikebrahim
  real_user_home: "/home/alikebrahim"
  ```
- **Replace throughout playbook:**
  - `ansible_user_id` -> `real_user`
  - `ansible_user_home` -> `real_user_home`
  - Tasks referencing `lookup('env', 'HOME')` -> hardcoded `real_user_home` (ensures consistency even with `become: true`)

### 3. Task Audits: User vs. System

#### **Roles Needing Splits or Rewrites:**

| Role         | Action |
|--------------|--------|
| **development** | Split tasks into user/system:
  - User: `languages.yml` (nvm, cargo, pyenv setup), `repositories.yml` (personal repos), `github.yml` (GH CLI config)
  - System: package installs, build tools setup, `/usr/local` modifications |
| **apps**         |
  - Ensure `binaries.yml`, `main.yml`, `browsers.yml` run with `become: false`.
  - Obsidian/Logseq AppImage tasks stay in user play |
| **common**       | Remains in system play |
| **pop_os**       | Remains in system play |
| **dotfiles**     | User play only. Fix ownership, avoid become. |
| **shell**        | User play only. `atuin`, `tldr`, ZSH changes stay user-level. |
| **terminal**     | System-level for `update-alternatives`. User-level for configs, if applicable. |
| **fonts**        | User play only. Font installation & `fc-cache` must run as the user. |

### 4. File & Task-Level Corrections

#### **Become/Ownership Fixes:**

- All `file`, `copy`, `pip`, `command`, and `shell` tasks acting on `$HOME` should have:
  ```yaml
  become: false
  owner: "{{ real_user }}"
  group: "{{ real_user }}"
  ```

- All pip/npm installs must have `become: false` explicitly.

- Any `ansible.builtin.shell` invoking installers (nvm, rustup) should set:
  ```yaml
  become: false
  environment:
    HOME: "{{ real_user_home }}"
    USER: "{{ real_user }}"
  ```

#### SSH
- Remove SSH key related vars/ tasks, where applicable

### 5. Role Metadata Updates
- Split `development/meta/main.yml` into two sections:
  - `development_user/meta/main.yml`
  - `development_system/meta/main.yml`
- Adjust `requirements.yml` if any external roles get introduced during refactor.

### 6. Molecule Test
- Remove everything related to molecule tests

---

## Important Considerations

### A. Ansible Version Compatibility
- Target Ansible **2.17+**, validate module support (`systemd_service`, `pip`, etc.).
- Ensure **fully-qualified module names** are preserved.

### B. Safety Nets
- Use **`changed_when`** and **`failed_when`** appropriately to avoid misleading output.
- **Back up `$HOME`** before applying the refactored playbook.

### C. Debug Enhancements
- Add `tags:` to tasks more aggressively for easy `--tags` or `--skip-tags` filtering.
- Implement verbose logging via `ansible.cfg` `log_path` for review.

---

## Conclusion
This restructuring provides:
- **Clear separation** of concerns
- **Safe user-level configuration**
- **Minimized risk** of root-level changes corrupting user space
- **Easier future maintenance** and task tracking

The two-play pattern aligns best with your playbook's dual focus (system and user) while retaining flexibility and clarity. Once refactored, future enhancements (e.g., multi-user support) become easier to implement.

