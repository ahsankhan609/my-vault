---
created: 2026-06-03
tags:
  - wsl
  - bash
  - commands
  - shortcuts
aliases:
  - wsl-commands
  - wsl-setup
---
[10 Bash History Shortcuts Every Linux User Should Know](10%20Bash%20History%20Shortcuts%20Every%20Linux%20User%20Should%20Know.md)
[Power Shell Commands - Equal to Linux Commands](Power%20Shell%20Commands%20-%20Equal%20to%20Linux%20Commands.md)

| Command                                | use case                                | Description                                                                            |
| -------------------------------------- | --------------------------------------- | -------------------------------------------------------------------------------------- |
| `wsl --update`                         |                                         | update WSL itself                                                                      |
| `wsl --version`                        |                                         | show the all version of the WSL system including Kernel and windows version            |
| `wsl --list --online`                  |                                         | list all available distros through WSL                                                 |
| `wsl --install`                        |                                         | Install WSL on windows and install Ubuntu as default distro                            |
| `wsl --list --verbose`                 |                                         | list all installed Distros, with Name, State(Running or Stopped) and Version           |
| `wsl --install -d <distribition_name>` |                                         | install specific distribution through WSL                                              |
| `wsl --install -d kali-linux`          | Install **Kali Linux** on Windows       |                                                                                        |
| `wsl --install -d Ubuntu-26.04`        | Install **Ubuntu 26.04 LTS** on windows |                                                                                        |
| `shutdown /r /t 0`                     |                                         | restart windows after installing distor                                                |
| `wsl --shutdown`                       |                                         | Shutdown(Stopped) all running distros                                                  |
| `wsl --unregister <distro_name>`       |                                         | Unregisters(remove-delete-uninstall) the distribution and deletes the root filesystem. |
|                                        |                                         | enable WSL with `systemd` functionality                                                |
