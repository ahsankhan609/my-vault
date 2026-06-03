---
created: 2026-06-03
tags:
  - commands
  - bash
  - power-shell
  - wsl
---
[WSL for windows - Installation - Setting up](WSL%20for%20windows%20-%20Installation%20-%20Setting%20up.md)
[10 Bash History Shortcuts Every Linux User Should Know](10%20Bash%20History%20Shortcuts%20Every%20Linux%20User%20Should%20Know.md)


| Linux Command | Power Shell Command           | Description             | Use case                                   |
| ------------- | ----------------------------- | ----------------------- | ------------------------------------------ |
| `grep`        | `Select-String` / `sls`       | filter text from result | `wsl --help \| Select-String "unregister"` |
| `cat`         | `Get-Content` / `gc`          | read file               |                                            |
| `ls`          | `Get-Children` / `ls`         | see files               |                                            |
| `rm -rf`      | `Remove-Item -Recurse -Force` | delete                  |                                            |
| `which`       | `Get-Command`                 | command path            |                                            |
