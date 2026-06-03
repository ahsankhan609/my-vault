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


| Linux Command | Power Shell Command           | Description                                                                                                                                                  | Use case                                   |
| ------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| `grep`        | `Select-String` / `sls`       | filter text from result                                                                                                                                      | `wsl --help \| Select-String "unregister"` |
| `cat`         | `Get-Content` / `gc`          | read file                                                                                                                                                    |                                            |
| `ls`          | `Get-Children` / `ls`         | see files                                                                                                                                                    |                                            |
| `rm -rf`      | `Remove-Item -Recurse -Force` | delete                                                                                                                                                       |                                            |
| `which`       | `Get-Command`                 | command path                                                                                                                                                 |                                            |
| `apt upgrade` | `winget upgrade --all`        | checks all software installed on your system (not just winget-installed ones) and upgrades any that have a newer version available in the winget repository. | `winget upgrade --all`                     |
|               | `winget upgrade`              | just LIST what has updates, without installing                                                                                                               | `winget upgrade`                           |

#### `winget` - details

The winget upgrade --all command checks all software installed on your system (not just winget-installed ones) and upgrades any that have a newer version available in the winget repository.

What it does step by step:

1. Scans all installed programs on your PC
2. Compares each against the latest versions in winget's package database
3. Downloads and installs updates for everything that has one

Key things to know:

- It's not automatic — you run it manually whenever you want to update
- It can update non-winget apps too — like Chrome, VS Code, 7-Zip, etc., as long as winget recognizes them
- It may ask for admin permission for some packages during the process
- Some packages may be skipped if they have their own built-in updater (winget will flag them as "unknown" version)

Useful variations:

winget upgrade --all --silent        # no prompts, fully quiet
winget upgrade --all --include-unknown  # try to upgrade even "unknown" version packages
winget upgrade                       # just LIST what has updates, without installing

Think of it like a Windows equivalent of apt upgrade on Linux — one command to update everything. Many people run it occasionally to keep their system up to date.

**can we upgrade single program**

Yes! Once winget upgrade lists all upgradable programs, you can upgrade a single one by specifying its ID:

`winget upgrade <ID>`

Example:

Running winget upgrade might show output like this:
|Name|ID|Version Available|
|---|---|---|
|Node.js LTS|OpenJS.NodeJS.LTS|24.16.0|24.17.0|
|Google Chrome|Google.Chrome|120.0|121.0|
|VS Code|Microsoft.VisualStudioCode|1.85|1.86|

To upgrade only VS Code:
`winget upgrade Microsoft.VisualStudioCode`

To upgrade only Node.js:
`winget upgrade OpenJS.NodeJS.LTS`

Tips:

- The ID column is what you pass to the command — it's unique and precise
- If you're unsure of the exact ID, you can also use the name (less reliable):
`winget upgrade "Google Chrome"`
- Add --silent to skip any prompts:
`winget upgrade OpenJS.NodeJS.LTS --silent`

So the workflow is: run winget upgrade to see the list, then pick the ID of whatever you want to update.