---
aliases:
  - bash-alias
created: 2026-06-14
tags:
  - linux
  - alias
  - shortcuts
  - commands
  - power-shell
blog-1: https://linuxvox.com/blog/how-to-create-bash-aliases/
blog-2: https://sysadminsage.com/how-to-create-alias-in-linux/
---
**Listing Aliases**

```bash
alias
```

**To view a specific alias:**

```bash
alias ll  # Shows the definition of the `ll` alias
```

**Permanent Removal**

```bash
vi ~/.bashrc
# delete the alias line
source ~/.bashrc
```

**Step 1: Open the File in a Text Editor**

```bash
vi ~/.bashrc
```

**Step 2: Add Your Alias**

```bash
# Custom aliases
alias ll='ls -lha'    # List all files in long format (human-readable)
alias c='clear'    # Clear the terminal
alias update='sudo apt update && sudo apt upgrade -y'  # Update system packages
```

**Step 3: Save and Exit**

**Step 4 : Sourcing the Configuration File**

**To load the updated ~/.bashrc immediately, "source" it with:**

```bash
source ~/.bashrc
# Or, shorter:
. ~/.bashrc
```

**Practical Alias Examples**

```bash
alias c='clear'    # Clear terminal
alias h='history'    # Show command history
alias ..='cd ..'    # Go up one directory
alias ...='cd ../../'    # Go up two directories
alias ~='cd ~'    # Go to home directory
```