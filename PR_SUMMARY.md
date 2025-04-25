# Pull Request: Refactor Ansible Playbook to Two-Play Architecture

This PR implements a comprehensive refactoring of the Ansible playbook to follow a two-play architecture that clearly separates system-level operations from user-level operations. This improves security, maintainability, and prevents unintended system-wide changes.

## Core Changes

1. **Two-Play Architecture**
   - Created separate System Play (with `become: true`) for system-wide operations
   - Created separate User Play (with `become: false`) for user environment setup
   - Each role now operates in the appropriate context

2. **Variable Standardization**
   - Added `real_user` and `real_user_home` variables for consistent identification
   - Replaced all instances of `ansible_user_id` with `real_user`
   - Replaced all instances of `ansible_user_home` with `real_user_home`

3. **Role Refactoring**
   - Development role split into system and user tasks
   - Apps role properly configured for user context
   - All user-level roles moved to user play
   - Fixed file ownership permissions

4. **Enhanced Tagging System**
   - Added context-aware tags (`system` and `user`)
   - Tasks can be selectively executed in specific contexts

## Detailed Changes

### Playbook Structure
- Modified `local.ansible.yml` to have two separate plays
- Added proper context check conditions to roles

### Variable Management
- Updated `group_vars/all.yml` with new variable definitions
- Mapped legacy variables to new ones for backward compatibility

### Role Reorganization
- **Development Role**: Created separate task files in system/ and user/ directories
- **Common Role**: Modified to work in both contexts
- **Apps Role**: Ensures proper user context for installations
- **Pop_OS Role**: Explicitly tagged as system-level
- **Dotfiles/Shell/Terminal/Fonts Roles**: Explicitly configured as user-level

### Permissions & Ownership
- Added explicit ownership restoration after privileged operations
- Fixed file permissions to prevent root-owned files in home directory
- Ensured environment variables are properly set in user context

### Documentation
- Updated README.md with new architecture
- Added new tagging documentation
- Created role context map

## Testing
- Verified syntax and execution in check mode
- Tested individual roles with specific tags
- Ran full playbook in check mode

## Benefits

1. **Security**: Follows principle of least privilege
2. **Maintainability**: Clear separation of concerns
3. **Safety**: Prevents accidental system-wide changes
4. **Usability**: Context-aware tagging for selective execution
5. **Compatibility**: Maintains backward compatibility

## How to Test
1. Run with check mode: `ansible-playbook local.ansible.yml --check --diff`
2. Test system context: `ansible-playbook local.ansible.yml --tags "system" --check`
3. Test user context: `ansible-playbook local.ansible.yml --tags "user" --check`