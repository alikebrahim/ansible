INSTRUCTIONS: Below are the details of the errors enountered during a run. Note it to proceed with instructions, then report it in ./Comments.md. Once done, clear the error report from this template:

TASK [development : Check if Node.js is installed] ******************************************************************************************************************************************************
Thursday 27 March 2025  11:49:16 +0300 (0:00:03.890)       0:00:32.218 ********
fatal: [localhost]: FAILED! => {"changed": false, "cmd": "node --version", "msg": "[Errno 2] No such file or directory: b'node'", "rc": 2, "stderr": "", "stderr_lines": [], "stdout": "", "stdout_lines": []}
...ignoring
 
TASK [development : Clone personal repositories] ********************************************************************************************************************************************************
Thursday 27 March 2025  11:50:27 +0300 (0:01:10.527)       0:01:43.111 ********
failed: [localhost] (item={'repo': 'git@github.com:alikebrahim/obsidian-silo.git', 'dest': '/home/alikebrahim/Documents/obsidian'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git ls-remote git@github.com:alikebrahim/obsidian-silo.git -h refs/heads/HEAD", "item": {"dest": "/home/alikebrahim/Documents/obsidian", "repo": "git@github.com:alikebrahim/obsidian-silo.git"}, "msg": "Host key verification failed.\r\nfatal: Could not read from remote repository.\n\nPlease make sure you have the correct access rights\nand the repository exists.", "rc": 128, "stderr": "Host key verification failed.\r\nfatal: Could not read from remote repository.\n\nPlease make sure you have the correct access rights\nand the repository exists.\n", "stderr_lines": ["Host key verification failed.", "fatal: Could not read from remote repository.", "", "Please make sure you have the correct access rights", "and the repository exists."], "stdout": "", "stdout_lines": []}
failed: [localhost] (item={'repo': 'git@github.com:alikebrahim/books.git', 'dest': '/home/alikebrahim/Documents/books'}) => {"ansible_loop_var": "item", "changed": false, "cmd": "/usr/bin/git ls-remote git@github.com:alikebrahim/books.git -h refs/heads/HEAD", "item": {"dest": "/home/alikebrahim/Documents/books", "repo": "git@github.com:alikebrahim/books.git"}, "msg": "Host key verification failed.\r\nfatal: Could not read from remote repository.\n\nPlease make sure you have the correct access rights\nand the repository exists.", "rc": 128, "stderr": "Host key verification failed.\r\nfatal: Could not read from remote repository.\n\nPlease make sure you have the correct access rights\nand the repository exists.\n", "stderr_lines": ["Host key verification failed.", "fatal: Could not read from remote repository.", "", "Please make sure you have the correct access rights", "and the repository exists."], "stdout": "", "stdout_lines": []}


TASK [common : Include SSH setup] ***********************************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.349)       0:00:01.313 ********
included: /home/alikebrahim/ansible/roles/common/tasks/ssh.yml for localhost

TASK [common : Ensure .ssh directory exists] ************************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.017)       0:00:01.330 ********
ok: [localhost]

TASK [common : Install SSH private key from vault] ******************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.147)       0:00:01.478 ********
skipping: [localhost]

TASK [common : Install SSH private key from file] *******************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.014)       0:00:01.492 ********
skipping: [localhost]

TASK [common : Install SSH public key from vault] *******************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.016)       0:00:01.508 ********
skipping: [localhost]

TASK [common : Install SSH public key from file] ********************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.020)       0:00:01.529 ********
skipping: [localhost]

TASK [common : Add GitHub to known_hosts file] **********************************************************************************************************************************************************
Thursday 27 March 2025  11:48:46 +0300 (0:00:00.021)       0:00:01.550 ********
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
# github.com:22 SSH-2.0-582030191
ok: [localhost]

TASK [common : Add SSH key to agent] ********************************************************************************************************************************************************************
Thursday 27 March 2025  11:48:54 +0300 (0:00:08.482)       0:00:10.032 ********
skipping: [localhost]
