Run 1:
alikebrahim@pop-os:~/ansible$ ansible-playbook local.ansible.yml --ask-become-pass --ask-vault-pass
BECOME password: 
Vault password: 

PLAY [Configure Personal Workstation] ******************************************

TASK [Gathering Facts] *********************************************************
Wednesday 26 March 2025  23:32:38 +0300 (0:00:00.017)       0:00:00.017 ******* 
ok: [localhost]

TASK [Install required Ansible collections] ************************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.856)       0:00:00.874 ******* 
ok: [localhost]

TASK [common : Include SSH setup] **********************************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.405)       0:00:01.279 ******* 
included: /home/alikebrahim/ansible/roles/common/tasks/ssh.yml for localhost

TASK [common : Ensure .ssh directory exists] ***********************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.017)       0:00:01.296 ******* 
changed: [localhost]

TASK [common : Install SSH private key from vault] *****************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.150)       0:00:01.446 ******* 
skipping: [localhost]

TASK [common : Install SSH private key from file] ******************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.015)       0:00:01.462 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from vault] ******************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.013)       0:00:01.476 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from file] *******************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.020)       0:00:01.496 ******* 
skipping: [localhost]

TASK [common : Add GitHub to known_hosts file] *********************************
Wednesday 26 March 2025  23:32:39 +0300 (0:00:00.016)       0:00:01.513 ******* 
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
changed: [localhost]

TASK [common : Add SSH key to agent] *******************************************
Wednesday 26 March 2025  23:32:41 +0300 (0:00:02.183)       0:00:03.696 ******* 
skipping: [localhost]

TASK [common : Check if Tailscale is installed] ********************************
Wednesday 26 March 2025  23:32:42 +0300 (0:00:00.019)       0:00:03.715 ******* 
fatal: [localhost]: FAILED! => {"changed": false, "cmd": "tailscale version", "msg": "[Errno 2] No such file or directory: b'tailscale'", "rc": 2, "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
...ignoring

TASK [common : Install Tailscale] **********************************************
Wednesday 26 March 2025  23:32:42 +0300 (0:00:00.099)       0:00:03.815 ******* 
changed: [localhost]

TASK [common : Create directory for apt keyrings] ******************************
Wednesday 26 March 2025  23:32:55 +0300 (0:00:12.970)       0:00:16.785 ******* 
ok: [localhost]

TASK [common : Add 1Password GPG key] ******************************************
Wednesday 26 March 2025  23:32:55 +0300 (0:00:00.101)       0:00:16.886 ******* 
changed: [localhost]

TASK [common : Add 1Password repository] ***************************************
Wednesday 26 March 2025  23:32:55 +0300 (0:00:00.493)       0:00:17.379 ******* 
fatal: [localhost]: FAILED! => {"changed": false, "msg": "Failed to lock directory /var/lib/apt/lists/: E:Could not get lock /var/lib/apt/lists/lock. It is held by process 1195 (packagekitd)"}

PLAY RECAP *********************************************************************
localhost                  : ok=9    changed=4    unreachable=0    failed=1    skipped=5    rescued=0    ignored=1   

Wednesday 26 March 2025  23:33:06 +0300 (0:00:10.880)       0:00:28.260 ******* 
=============================================================================== 
common : Install Tailscale --------------------------------------------- 12.97s
common : Add 1Password repository -------------------------------------- 10.88s
common : Add GitHub to known_hosts file --------------------------------- 2.18s
Gathering Facts --------------------------------------------------------- 0.86s
common : Add 1Password GPG key ------------------------------------------ 0.49s
Install required Ansible collections ------------------------------------ 0.41s
common : Ensure .ssh directory exists ----------------------------------- 0.15s
common : Create directory for apt keyrings ------------------------------ 0.10s
common : Check if Tailscale is installed -------------------------------- 0.10s
common : Install SSH public key from vault ------------------------------ 0.02s
common : Add SSH key to agent ------------------------------------------- 0.02s
common : Include SSH setup ---------------------------------------------- 0.02s
common : Install SSH public key from file ------------------------------- 0.02s
common : Install SSH private key from vault ----------------------------- 0.02s
common : Install SSH private key from file ------------------------------ 0.01s

Run 2:
These tasks failed. Removed along with relevant tasks
TASK [common : Check if Tailscale is installed] ********************************
TASK [common : Add 1Password repository] ***************************************
tailscale and 1password tasks removed
alikebrahim@pop-os:~/ansible$ ansible-playbook local.ansible.yml --ask-become-pass --ask-vault-pass
BECOME password: 
Vault password: 

PLAY [Configure Personal Workstation] ********************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:18 +0300 (0:00:00.014)       0:00:00.014 ******* 
ok: [localhost]

TASK [Install required Ansible collections] **************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:18 +0300 (0:00:00.761)       0:00:00.775 ******* 
ok: [localhost]

TASK [common : Include SSH setup] ************************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.384)       0:00:01.160 ******* 
included: /home/alikebrahim/ansible/roles/common/tasks/ssh.yml for localhost

TASK [common : Ensure .ssh directory exists] *************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.018)       0:00:01.178 ******* 
ok: [localhost]

TASK [common : Install SSH private key from vault] *******************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.146)       0:00:01.325 ******* 
skipping: [localhost]

TASK [common : Install SSH private key from file] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.015)       0:00:01.340 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from vault] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.018)       0:00:01.359 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from file] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.016)       0:00:01.376 ******* 
skipping: [localhost]

TASK [common : Add GitHub to known_hosts file] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.014)       0:00:01.391 ******* 
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
ok: [localhost]

TASK [common : Add SSH key to agent] *********************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:02.176)       0:00:03.568 ******* 
skipping: [localhost]

TASK [common : Create directory for apt keyrings] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:00.018)       0:00:03.586 ******* 
ok: [localhost]

TASK [common : Configure sudoers with template] **********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:00.109)       0:00:03.695 ******* 
changed: [localhost]

TASK [development : Download GitHub CLI GPG key] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:22 +0300 (0:00:00.278)       0:00:03.974 ******* 
changed: [localhost]

TASK [development : Add GitHub CLI repository] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:22 +0300 (0:00:00.557)       0:00:04.531 ******* 
changed: [localhost]

TASK [development : Install GitHub CLI] ******************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:27 +0300 (0:00:04.473)       0:00:09.004 ******* 
changed: [localhost]

TASK [development : Check if Node.js is installed] *******************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:03.227)       0:00:12.232 ******* 
fatal: [localhost]: FAILED! => {"changed": false, "cmd": "node --version", "msg": "[Errno 2] No such file or directory: b'node'", "rc": 2, "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
...ignoring

TASK [development : Install Claude-Code] *****************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.100)       0:00:12.333 ******* 
skipping: [localhost]

TASK [development : Include repositories tasks] **********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.013)       0:00:12.347 ******* 
included: /home/alikebrahim/ansible/roles/development/tasks/repositories.yml for localhost

TASK [development : Ensure project directories exist] ****************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.020)       0:00:12.367 ******* 
changed: [localhost] => (item=/root/.local/src)
changed: [localhost] => (item=/root/Documents)

TASK [development : Clone development tool repositories] *************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.197)       0:00:12.565 ******* 
failed: [localhost] (item={'repo': 'https://github.com/neovim/neovim', 'dest': '/root/.local/src/neovim'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/neovim/neovim /root/.local/src/neovim", "item": {"dest": "/root/.local/src/neovim", "repo": "https://github.com/neovim/neovim"}, "msg": "fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/tmux/tmux.git', 'dest': '/root/.local/src/tmux'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/tmux/tmux.git /root/.local/src/tmux", "item": {"dest": "/root/.local/src/tmux", "repo": "https://github.com/tmux/tmux.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/aristocratos/btop.git', 'dest': '/root/.local/src/btop'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/aristocratos/btop.git /root/.local/src/btop", "item": {"dest": "/root/.local/src/btop", "repo": "https://github.com/aristocratos/btop.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/btop': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/btop': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/btop': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/junegunn/fzf.git', 'dest': '/root/.local/src/fzf', 'depth': 1}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin --depth 1 https://github.com/junegunn/fzf.git /root/.local/src/fzf", "item": {"depth": 1, "dest": "/root/.local/src/fzf", "repo": "https://github.com/junegunn/fzf.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied"], "stdout": "", "stdout_lines": []}

PLAY RECAP ***********************************************************************************************************************************************************************************
localhost                  : ok=13   changed=5    unreachable=0    failed=1    skipped=6    rescued=0    ignored=1   

Wednesday 26 March 2025  23:41:36 +0300 (0:00:05.368)       0:00:17.934 ******* 
=============================================================================== 
development : Clone development tool repositories ------------------------------------------------------------------------------------------------------------------------------------- 5.37s
development : Add GitHub CLI repository ----------------------------------------------------------------------------------------------------------------------------------------------- 4.47s
development : Install GitHub CLI ------------------------------------------------------------------------------------------------------------------------------------------------------ 3.23s
common : Add GitHub to known_hosts file ----------------------------------------------------------------------------------------------------------------------------------------------- 2.18s
Gathering Facts ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- 0.76s
development : Download GitHub CLI GPG key --------------------------------------------------------------------------------------------------------------------------------------------- 0.56s
Install required Ansible collections -------------------------------------------------------------------------------------------------------------------------------------------------- 0.38s
common : Configure sudoers with template ---------------------------------------------------------------------------------------------------------------------------------------------- 0.28s
development : Ensure project directories exist ---------------------------------------------------------------------------------------------------------------------------------------- 0.20s
common : Ensure .ssh directory exists ------------------------------------------------------------------------------------------------------------------------------------------------- 0.15s
common : Create directory for apt keyrings -------------------------------------------------------------------------------------------------------------------------------------------- 0.11s
development : Check if Node.js is installed ------------------------------------------------------------------------------------------------------------------------------------------- 0.10s
development : Include repositories tasks ---------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH private key from file -------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Include SSH setup ------------------------------------------------------------------------------------------------------------------------------------------------------------ 0.02s
common : Add SSH key to agent --------------------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH public key from vault -------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH private key from vault ------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH public key from file --------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
development : Install Claude-Code ----------------------------------------------------------------------------------------------------------------------------------------------------- 0.01s

Run 3:
These tasks failed. Removed along with relevant tasks
TASK [development : Check if Node.js is installed] *******************************************************************************************************************************************
TASK [development : Clone development tool repositories] *************************************************************************************************************************************
alikebrahim@pop-os:~/ansible$ ansible-playbook local.ansible.yml --ask-become-pass --ask-vault-pass
BECOME password: 
Vault password: 

PLAY [Configure Personal Workstation] ********************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:18 +0300 (0:00:00.014)       0:00:00.014 ******* 
ok: [localhost]

TASK [Install required Ansible collections] **************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:18 +0300 (0:00:00.761)       0:00:00.775 ******* 
ok: [localhost]

TASK [common : Include SSH setup] ************************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.384)       0:00:01.160 ******* 
included: /home/alikebrahim/ansible/roles/common/tasks/ssh.yml for localhost

TASK [common : Ensure .ssh directory exists] *************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.018)       0:00:01.178 ******* 
ok: [localhost]

TASK [common : Install SSH private key from vault] *******************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.146)       0:00:01.325 ******* 
skipping: [localhost]

TASK [common : Install SSH private key from file] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.015)       0:00:01.340 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from vault] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.018)       0:00:01.359 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from file] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.016)       0:00:01.376 ******* 
skipping: [localhost]

TASK [common : Add GitHub to known_hosts file] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:19 +0300 (0:00:00.014)       0:00:01.391 ******* 
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
ok: [localhost]

TASK [common : Add SSH key to agent] *********************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:02.176)       0:00:03.568 ******* 
skipping: [localhost]

TASK [common : Create directory for apt keyrings] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:00.018)       0:00:03.586 ******* 
ok: [localhost]

TASK [common : Configure sudoers with template] **********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:21 +0300 (0:00:00.109)       0:00:03.695 ******* 
changed: [localhost]

TASK [development : Download GitHub CLI GPG key] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:22 +0300 (0:00:00.278)       0:00:03.974 ******* 
changed: [localhost]

TASK [development : Add GitHub CLI repository] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:22 +0300 (0:00:00.557)       0:00:04.531 ******* 
changed: [localhost]

TASK [development : Install GitHub CLI] ******************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:27 +0300 (0:00:04.473)       0:00:09.004 ******* 
changed: [localhost]

TASK [development : Check if Node.js is installed] *******************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:03.227)       0:00:12.232 ******* 
fatal: [localhost]: FAILED! => {"changed": false, "cmd": "node --version", "msg": "[Errno 2] No such file or directory: b'node'", "rc": 2, "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
...ignoring

TASK [development : Install Claude-Code] *****************************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.100)       0:00:12.333 ******* 
skipping: [localhost]

TASK [development : Include repositories tasks] **********************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.013)       0:00:12.347 ******* 
included: /home/alikebrahim/ansible/roles/development/tasks/repositories.yml for localhost

TASK [development : Ensure project directories exist] ****************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.020)       0:00:12.367 ******* 
changed: [localhost] => (item=/root/.local/src)
changed: [localhost] => (item=/root/Documents)

TASK [development : Clone development tool repositories] *************************************************************************************************************************************
Wednesday 26 March 2025  23:41:30 +0300 (0:00:00.197)       0:00:12.565 ******* 
failed: [localhost] (item={'repo': 'https://github.com/neovim/neovim', 'dest': '/root/.local/src/neovim'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/neovim/neovim /root/.local/src/neovim", "item": {"dest": "/root/.local/src/neovim", "repo": "https://github.com/neovim/neovim"}, "msg": "fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/neovim': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/tmux/tmux.git', 'dest': '/root/.local/src/tmux'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/tmux/tmux.git /root/.local/src/tmux", "item": {"dest": "/root/.local/src/tmux", "repo": "https://github.com/tmux/tmux.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/tmux': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/aristocratos/btop.git', 'dest': '/root/.local/src/btop'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin https://github.com/aristocratos/btop.git /root/.local/src/btop", "item": {"dest": "/root/.local/src/btop", "repo": "https://github.com/aristocratos/btop.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/btop': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/btop': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/btop': Permission denied"], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'https://github.com/junegunn/fzf.git', 'dest': '/root/.local/src/fzf', 'depth': 1}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git clone --origin origin --depth 1 https://github.com/junegunn/fzf.git /root/.local/src/fzf", "item": {"depth": 1, "dest": "/root/.local/src/fzf", "repo": "https://github.com/junegunn/fzf.git"}, "msg": "fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied", "rc": 128, "stderr": "fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied\n", "stderr_lines": ["fatal: could not create leading directories of '/root/.local/src/fzf': Permission denied"], "stdout": "", "stdout_lines": []}

PLAY RECAP ***********************************************************************************************************************************************************************************
localhost                  : ok=13   changed=5    unreachable=0    failed=1    skipped=6    rescued=0    ignored=1   

Wednesday 26 March 2025  23:41:36 +0300 (0:00:05.368)       0:00:17.934 ******* 
=============================================================================== 
development : Clone development tool repositories ------------------------------------------------------------------------------------------------------------------------------------- 5.37s
development : Add GitHub CLI repository ----------------------------------------------------------------------------------------------------------------------------------------------- 4.47s
development : Install GitHub CLI ------------------------------------------------------------------------------------------------------------------------------------------------------ 3.23s
common : Add GitHub to known_hosts file ----------------------------------------------------------------------------------------------------------------------------------------------- 2.18s
Gathering Facts ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- 0.76s
development : Download GitHub CLI GPG key --------------------------------------------------------------------------------------------------------------------------------------------- 0.56s
Install required Ansible collections -------------------------------------------------------------------------------------------------------------------------------------------------- 0.38s
common : Configure sudoers with template ---------------------------------------------------------------------------------------------------------------------------------------------- 0.28s
development : Ensure project directories exist ---------------------------------------------------------------------------------------------------------------------------------------- 0.20s
common : Ensure .ssh directory exists ------------------------------------------------------------------------------------------------------------------------------------------------- 0.15s
common : Create directory for apt keyrings -------------------------------------------------------------------------------------------------------------------------------------------- 0.11s
development : Check if Node.js is installed ------------------------------------------------------------------------------------------------------------------------------------------- 0.10s
development : Include repositories tasks ---------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH private key from file -------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Include SSH setup ------------------------------------------------------------------------------------------------------------------------------------------------------------ 0.02s
common : Add SSH key to agent --------------------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH public key from vault -------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH private key from vault ------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Install SSH public key from file --------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
development : Install Claude-Code ----------------------------------------------------------------------------------------------------------------------------------------------------- 0.01s

Run 4:
These tasks failed. Removed along with relevant tasks:
TASK [development : Install Claude-Code] *****************************************************************************************************************************************************
alikebrahim@pop-os:~/ansible$ ansible-playbook local.ansible.yml --ask-become-pass --ask-vault-pass
BECOME password: 
Vault password: 

PLAY [Configure Personal Workstation] ********************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:12 +0300 (0:00:00.014)       0:00:00.014 ******* 
ok: [localhost]

TASK [Install required Ansible collections] **************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:12 +0300 (0:00:00.793)       0:00:00.807 ******* 
ok: [localhost]

TASK [common : Include SSH setup] ************************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.369)       0:00:01.177 ******* 
included: /home/alikebrahim/ansible/roles/common/tasks/ssh.yml for localhost

TASK [common : Ensure .ssh directory exists] *************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.018)       0:00:01.196 ******* 
ok: [localhost]

TASK [common : Install SSH private key from vault] *******************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.166)       0:00:01.362 ******* 
skipping: [localhost]

TASK [common : Install SSH private key from file] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.013)       0:00:01.376 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from vault] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.013)       0:00:01.389 ******* 
skipping: [localhost]

TASK [common : Install SSH public key from file] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.011)       0:00:01.401 ******* 
skipping: [localhost]

TASK [common : Add GitHub to known_hosts file] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:13 +0300 (0:00:00.013)       0:00:01.414 ******* 
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
ok: [localhost]

TASK [common : Add SSH key to agent] *********************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:15 +0300 (0:00:02.189)       0:00:03.604 ******* 
skipping: [localhost]

TASK [common : Create directory for apt keyrings] ********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:15 +0300 (0:00:00.021)       0:00:03.625 ******* 
ok: [localhost]

TASK [common : Configure sudoers with template] **********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:15 +0300 (0:00:00.103)       0:00:03.729 ******* 
ok: [localhost]

TASK [development : Download GitHub CLI GPG key] *********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:16 +0300 (0:00:00.266)       0:00:03.995 ******* 
ok: [localhost]

TASK [development : Add GitHub CLI repository] ***********************************************************************************************************************************************
Wednesday 26 March 2025  23:48:16 +0300 (0:00:00.246)       0:00:04.242 ******* 
ok: [localhost]

TASK [development : Install GitHub CLI] ******************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:16 +0300 (0:00:00.230)       0:00:04.473 ******* 
ok: [localhost]

TASK [development : Install Claude-Code] *****************************************************************************************************************************************************
Wednesday 26 March 2025  23:48:16 +0300 (0:00:00.438)       0:00:04.911 ******* 
fatal: [localhost]: FAILED! => {"msg": "The conditional check 'node_version.rc == 0' failed. The error was: error while evaluating conditional (node_version.rc == 0): 'node_version' is undefined\n\nThe error appears to be in '/home/alikebrahim/ansible/roles/development/tasks/main.yml': line 26, column 3, but may\nbe elsewhere in the file depending on the exact syntax problem.\n\nThe offending line appears to be:\n\n\n- name: Install Claude-Code\n  ^ here\n"}

PLAY RECAP ***********************************************************************************************************************************************************************************
localhost                  : ok=10   changed=0    unreachable=0    failed=1    skipped=5    rescued=0    ignored=0   

Wednesday 26 March 2025  23:48:16 +0300 (0:00:00.008)       0:00:04.920 ******* 
=============================================================================== 
common : Add GitHub to known_hosts file ----------------------------------------------------------------------------------------------------------------------------------------------- 2.19s
Gathering Facts ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- 0.79s
development : Install GitHub CLI ------------------------------------------------------------------------------------------------------------------------------------------------------ 0.44s
Install required Ansible collections -------------------------------------------------------------------------------------------------------------------------------------------------- 0.37s
common : Configure sudoers with template ---------------------------------------------------------------------------------------------------------------------------------------------- 0.27s
development : Download GitHub CLI GPG key --------------------------------------------------------------------------------------------------------------------------------------------- 0.25s
development : Add GitHub CLI repository ----------------------------------------------------------------------------------------------------------------------------------------------- 0.23s
common : Ensure .ssh directory exists ------------------------------------------------------------------------------------------------------------------------------------------------- 0.17s
common : Create directory for apt keyrings -------------------------------------------------------------------------------------------------------------------------------------------- 0.10s
common : Add SSH key to agent --------------------------------------------------------------------------------------------------------------------------------------------------------- 0.02s
common : Include SSH setup ------------------------------------------------------------------------------------------------------------------------------------------------------------ 0.02s
common : Install SSH private key from vault ------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
common : Install SSH private key from file -------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
common : Install SSH public key from file --------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
common : Install SSH public key from vault -------------------------------------------------------------------------------------------------------------------------------------------- 0.01s
development : Install Claude-Code ----------------------------------------------------------------------------------------------------------------------------------------------------- 0.01s



