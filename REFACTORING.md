# Ansible Playbook Refactoring Implementation Plan

This document outlines the step-by-step implementation plan for refactoring the ansible playbook according to the strategy defined in REFACTOR.md.

## Phase 1: Setup and Preparation

- [x] **Backup & Versioning**
  - [x] Create a new git branch `refactor/two-play-structure`
  - [ ] Backup current home directory configuration files
  - [ ] Take snapshot of current system state for comparison testing

- [x] **Variable Definition**
  - [x] Update `group_vars/all.yml` with `real_user` and `real_user_home` variables
  - [x] Create a mapping document of all instances where `ansible_user_id` and `ansible_user_home` are used

- [ ] **Test Environment**
  - [ ] Set up a test environment (VM or container) to validate changes
  - [ ] Create simple verification playbook to test user/system separation

## Phase 2: Split Playbook Structure

- [x] **Create Two-Play Structure**
  - [x] Refactor `local.ansible.yml` into two distinct plays as outlined
  - [x] Run basic syntax validation: `ansible-playbook local.ansible.yml --syntax-check`
  - [ ] Test with `--check --diff` to validate no unintended changes

- [ ] **Validate Base Structure**
  - [ ] Run playbook in check mode with basic tasks only
  - [ ] Verify hosts, connection, and privilege escalation settings

## Phase 3: Role Refactoring

### System-Level Roles

- [ ] **pop_os role**
  - [ ] Audit tasks for proper privilege escalation
  - [ ] Ensure all system-wide operations use `become: true`
  - [ ] Add appropriate tags for system-level operations

- [ ] **common role**
  - [ ] Refactor `ssh.yml` to remove unnecessary SSH key tasks
  - [ ] Review all tasks for proper privilege handling
  - [ ] Test with `--tags common --check --diff`

### User-Level Roles

- [x] **dotfiles role**
  - [x] Set explicit `become: false` for all tasks
  - [x] Fix file ownership using `real_user` variables
  - [ ] Test with `--tags dotfiles`

- [x] **shell role**
  - [x] Move to user play with `become: false`
  - [x] Update ZSH, atuin, and tldr configurations
  - [ ] Test with `--tags shell`

- [x] **terminal role**
  - [x] Separate system-level configuration (alternatives)
  - [x] Move user-level configs to user play
  - [ ] Test with `--tags terminal`

- [x] **fonts role**
  - [x] Set proper user context for font installation
  - [x] Ensure `fc-cache` runs as user
  - [ ] Test with `--tags fonts`

### Split Roles

- [x] **development role**
  - [x] Identify system vs. user tasks
  - [x] Create separate task files for system and user operations
  - [ ] Update `meta` dependencies for both contexts
  - [ ] Test with `--tags development`

- [x] **apps role**
  - [x] Review binary installations for proper privilege handling
  - [x] Ensure browser and AppImage installations run as user
  - [ ] Test with `--tags apps`

## Phase 4: Variable and Path Correction

- [ ] **Variable Usage Audit**
  - [ ] Replace all `ansible_user_id` with `real_user`
  - [ ] Replace all `ansible_user_home` with `real_user_home`
  - [ ] Fix all instances of `lookup('env', 'HOME')`

- [ ] **File Ownership & Permissions**
  - [ ] Audit all file operations for proper ownership
  - [ ] Ensure all `$HOME` operations run without privileges
  - [ ] Verify pip/npm/cargo installs run as user

## Phase 5: Testing and Validation

- [ ] **Incremental Testing**
  - [ ] Run playbook with `--check --diff --tags=ROLE` for each role
  - [ ] Perform live test on test environment for each role
  - [ ] Document any unexpected behavior

- [ ] **Full Playbook Testing**
  - [ ] Run complete playbook in check mode
  - [ ] Verify tag functionality for selective execution
  - [ ] Run full playbook on test environment

- [ ] **Regression Testing**
  - [ ] Verify all original functionality is preserved
  - [ ] Check for any root-owned files in `$HOME`
  - [ ] Ensure all applications still function correctly

## Phase 6: Finalization and Documentation

- [ ] **Cleanup**
  - [ ] Remove molecule test references
  - [ ] Clean up any temporary or backup files

- [ ] **Documentation**
  - [ ] Update README.md with new playbook structure
  - [ ] Document new tagging scheme
  - [ ] Update any variable documentation

- [ ] **Final Commit**
  - [ ] Squash interim commits if necessary
  - [ ] Create pull request with detailed changelog
  - [ ] Merge to master after successful testing

## Success Criteria

1. No root-owned files in user home directory
2. All user-specific tasks run with `become: false`
3. System-wide tasks are properly isolated
4. Playbook runs successfully with no errors
5. All original functionality is preserved
6. Tags work properly for selective execution

## Rollback Plan

If issues are encountered during implementation or testing:

1. Note the specific failure point and error messages
2. Revert to the previous working commit
3. Address issues in isolation before re-attempting
4. If necessary, restore from the home directory backup

## Implementation Timeline

- Phase 1-2: 1-2 days
- Phase 3: 3-5 days
- Phase 4: 1-2 days
- Phase 5: 2-3 days
- Phase 6: 1 day

Total estimated time: 8-13 days