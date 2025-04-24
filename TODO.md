# Completed Tasks

The following tasks have been implemented:

- FFmpeg - Added to roles/apps/tasks/binaries.yml
  - Downloads from https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-linux64-gpl.tar.xz
  - Extracts bin/* to ~/.local/bin
  - Copies man/man1/* to ~/.local/share/man/man1

- yt-dlp - Added to roles/apps/tasks/binaries.yml
  - Installed via pip: python3 -m pip install -U "yt-dlp[default]"

- transmission - Added to popos_tools_packages in group_vars/all.yml
  - Installed via apt

- tldr -u fix - Added to roles/pop_os/tasks/utilities.yml
  - Fixed permission issues for tldr updates

- nvme-cli - Added to popos_tools_packages in group_vars/all.yml
  - Installed via apt


# TODO:
- fix /home/alikebrahim/.local/bin perms. Currently it's being with owner root
