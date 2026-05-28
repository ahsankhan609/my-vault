---
title: 10 Bash History Shortcuts Every Linux User Should Know
source: https://www.tecmint.com/bash-shortcuts-stop-retyping-commands/
author:
  - "[[Ravi Saive]]"
published: 2026-04-28
created: 2026-05-26
description: In this guide, we'll explain what sudo !!, fc, and history shortcuts do, how to use them, and how to stop retyping long Linux commands from scratch.
tags:
  - "#bash"
  - "#shortcuts"
---
***You’ve been retyping the same long commands for years, but `sudo !!`, `!$`, `^old^new`, and a handful of Bash history tricks can cut that habit down to almost nothing and this guide covers every one of them with real examples.***

You type a long [apt command](https://www.tecmint.com/apt-command-in-linux/ "Must-Know APT Commands") to install a package, hit **Enter**, and the terminal shows back `Permission denied`. So you arrow-up, jump to the beginning of the line, type `sudo`, and hit **Enter** again.

That little dance takes maybe 5 seconds, but you do it a dozen times a day, and it adds up, and that’s just one pattern. There are at least 10 ways sysadmins waste time [retyping commands](https://www.tecmint.com/run-repeat-linux-command-every-x-seconds/ "Repeat a Linux Command Every Few Seconds") they’ve already typed, and most of them have a one-keystroke fix that Bash has shipped for decades.

These shortcuts live inside Bash’s history expansion system, a feature most Linux users walk right past because nobody explains it as a whole picture. Once you see how `!!`, `!$`, `!*`, and event designators fit together, you stop reaching for the arrow keys by default and start treating your command history as a searchable, reusable scratchpad.

In this guide, we’ll explain what `sudo !!`, `fc`, and history shortcuts do, how to use them, and how to stop retyping long Linux commands from scratch.

Get the **Learn Linux 7 Days Crash Course** free when you join 34,000+ Linux professionals reading every Thursday.

Check your email for a magic link to get started.

## 1\. sudo!!: Run the Last Command as Root

This is the one that everybody eventually discovers by accident, and then wonders why nobody told them sooner. When you type `sudo !!`, the `!!` expands to the full text of the last command you ran, and `sudo` runs it with root privileges.

The `sudo` prefix runs the command with root privileges, which is required for anything that touches system files, installs packages, or changes services.

```
apt install htop
```

**Output**:

```
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
```

Instead of arrowing up and prepending `sudo` manually, just type this:

```
sudo !!
```

**Output**:

```
sudo apt install htop
[sudo] password for ravi:
Reading package lists... Done
Building dependency tree... Done
htop is already the newest version (3.3.0-4build1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

Bash replaces `!!` with the literal text of your last command before passing anything to the shell, so what actually runs:

```
sudo apt install htop
```

If you see `sudo: !!: command not found`, your shell is not Bash or you are running this inside a non-interactive shell like `sh`. This feature is Bash-specific, and `zsh` has its own equivalent (`sudo $_` works differently, so check your shell with `echo $SHELL` first).

***What’s the most embarrassing command you’ve re-run by accident with `sudo !!`? [Drop it in the comments](#comments), no judgment here.***

## 2.!$: Reuse the Last Argument of the Previous Command

The `!$` expands to the last argument of the previous command, which is the one you want when you’ve just created or referenced a file path and need to operate on it again with a different command.

```
mkdir -p /etc/myapp/config
```

Now you want to change into that directory:

```
cd !$
```

**Output**:

```
cd /etc/myapp/config
```

Bash expands `!$` to `/etc/myapp/config` before running [cd command](https://www.tecmint.com/cd-command-in-linux/ "Stop Using Only cd: Learn pushd, popd, and zoxide in Linux"). So you create the directory and immediately land inside it without typing the path twice.

Same pattern works across many common workflows. You run `vim /etc/ssh/sshd_config`, save your changes, and want to check the file’s permissions next:

```
ls -l !$
```

**Output**:

```
ls -l /etc/ssh/sshd_config
-rw-r--r-- 1 root root 3287 Jan 15 09:22 /etc/ssh/sshd_config
```

The most common mistake here is confusing `!$` with `$_`. Both expand to the last argument of the previous command, but `$_` is a shell variable and works in more contexts including scripts, while `!$` is history expansion and works only interactively. For one-liner command chaining at the terminal, either works. For scripts, use `$_`.

***If you work with long file paths every day, the [100+ Essential Linux Commands](https://pro.tecmint.com/linux-commands-series/ "100+ Linux Commands Every User Should Know") course covers every command and argument pattern with real examples from real systems***.

## 3.!\*: Reuse All Arguments From the Previous Command

Where `!$` gives you the last argument, `!*` gives you all arguments from the previous command, which is useful when you run a command against a set of files and need to run a second command against the same set.

```
chmod 644 report.txt notes.txt config.yaml
```

Now you want to check who owns those same files:

```
ls -l !*
```

**Output**:

```
ls -l report.txt notes.txt config.yaml
-rw-r--r-- 1 ravi ravi  1024 Apr 10 11:30 config.yaml
-rw-r--r-- 1 ravi ravi  2048 Apr 10 11:28 notes.txt
-rw-r--r-- 1 ravi ravi  4096 Apr 10 11:25 report.txt
```

Bash drops the full argument list from your last command in place of `!*`, saving you from retyping all three filenames. If you had a typo in one of them and the previous command failed, the same typo rides along, so this is not a substitute for double-checking your arguments before you use them again.

***If this helped you, share this with a colleague who’s still copying file paths by hand every time they change commands***.

## 4\. ^old^new: Fix a Typo in the Last Command

This one is underused and almost magical once it becomes a habit. The `^old^new` syntax re-runs your last command with one string substituted. You type a long command with a typo, and instead of arrowing back up and hunting for the mistake, you just replace it inline.

```
systemctl restart ngnix
```

**Output**:

```
Failed to restart ngnix.service: Unit ngnix.service not found.
```

The service name is `nginx`, not `ngnix`, to fix it, run:

```
^ngnix^nginx
```

**Output**:

```
systemctl restart nginx
```

Bash reprints the corrected command and runs it immediately. No arrow key, no cursor movement. The substitution only replaces the first occurrence of the string, so if your typo appears twice in the command, only the first one gets fixed.

For a global replacement across the whole command, use `!!:gs/old/new` instead, but that syntax comes up rarely in practice.

If you see `bash: :s/ngnix/nginx: substitution failed`, it means the string you typed in the first `^` position does not appear anywhere in your last command. Check the exact text carefully, including spaces.

## 5.!number: Re-Run a Specific Command From History

Your shell keeps a numbered log of every command you’ve run, and `!number` lets you fire any of them by number without retyping.

First, check the list with [history command](https://www.tecmint.com/history-command-examples/ "Linux history Command"):

```
history
```

**Output**:

```
498  df -h
  499  lsblk
  500  mount /dev/sdb1 /mnt/data
  501  ls /mnt/data
  502  umount /mnt/data
  503  history
```

To re-run command 500:

```
!500
```

**Output**:

```
mount /dev/sdb1 /mnt/data
```

Bash prints the expanded command before running it, which gives you a half-second to catch anything wrong, which is particularly useful when you have a long [find](https://www.tecmint.com/35-practical-examples-of-linux-find-command/ "Linux Find Command") or [rsync command](https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/ "Rsync Command in Linux") from earlier in the session that you want to run again without scrolling up through dozens of lines.

***Warning: Running old commands by number is safe for read-only operations, but dangerous for anything destructive like [rm](https://www.tecmint.com/remove-directory-linux/ "rm Command: Remove a Directory and File"), [dd](https://www.tecmint.com/dd-command-examples/ "dd Command in Linux"), or `mkfs`***.

***How do you manage long command history in your team? Do you use shared history files, set `HISTSIZE`, or something else? [Tell us in the comments](#comments "Share Your Command History Setup")***.

## 6.!string: Re-Run the Last Command Starting With a String

Instead of hunting for the number, you can re-run the most recent command that started with a specific string by typing `!` followed by that string.

```
!mount
```

**Output**:

```
mount /dev/sdb1 /mnt/data
```

Bash searches backward through your history, finds the most recent command that started with mount, and runs it. This is faster than `history | grep mount` when you know the command is recent and you want to re-run it, not just find it.

The risk is that you might not know exactly what the last `mount` command was, especially in a long session. To preview without running, use `!mount:p` instead. The `:p` modifier prints the command to the terminal without executing it, so you can confirm before committing.

```
!mount:p
```

**Output**:

```
mount /dev/sdb1 /mnt/data
```

***If you work with SSH and remote servers a lot, our [SSH Course](https://pro.tecmint.com/ssh-complete-course/ "SSH Course for Beginners") covers terminal productivity for remote sessions across all 54 chapters, including history tricks that work over `tmux` and `screen`***.

## 7\. Ctrl+R: Reverse Search Through History

The `Ctrl+R` opens an incremental reverse search through your history. It’s the fastest way to find and re-run a long command you half-remember typing.

Press `Ctrl+R` and you see:

```
(reverse-i-search)\`':
```

Start typing any part of the command you’re looking for:

```
(reverse-i-search)\`rsync': rsync -avz --progress /home/ravi/ backup@192.168.1.10:/backups/
```

Bash matches against your history in real time. Press **Enter** to run the command as-is, press `Ctrl+R` again to cycle to the next older match, or press the right arrow key to land the command in the prompt for editing before you run it.

If you see (`failed reverse-i-search`), the string you typed does not match anything in your history. Try fewer characters or a different part of the command.

**Tip**: ***Set `HISTSIZE=10000` and `HISTFILESIZE=20000` in your `~/.bashrc` to keep more history available for `Ctrl+R` to search through***.

## 8\. Alt+. (or Esc+.): Cycle Through Last Arguments

The `Alt+.` inserts the last argument of the previous command, exactly like `!$`, but it’s interactive. Press it once and you get the last argument from your most recent command. Press it again and you get the last argument from the command before that. Keep pressing and you cycle backward through history.

This is the interactive version of `!$`, and many sysadmins prefer it because you can see what you’re about to insert before you run anything.

```
tar -czf backup.tar.gz /home/ravi/documents
```

On the next command, press `Alt+.` and the prompt fills in:

```
ls -lh /home/ravi/documents
```

Press `Alt+.` again and it cycles to the argument before that from your history. This works on any Linux terminal with readline support, which covers virtually every modern distro’s default Bash setup.

***Once you start using `Alt+.` instead of retyping paths, there’s no going back, so share this article with any sysadmin on your team who’s still arrow-keying through history***.

## 9\. fc: Open the Last Command in Your Editor

The `fc` stands for “ **fix command** ” and it opens your last command in `$EDITOR` so you can edit it and run it when you close the file, which is the right tool when a command is so long that `^old^new` feels fiddly.

```
fc
```

This drops you into `vim` (or whatever `$EDITOR` is set to) with your last command pre-loaded. Edit it, save, and quit. Bash runs the updated command immediately.

You can also pass a range of history line numbers to `fc` to open multiple commands for editing as a script:

```
fc 498 501
```

**Output**:

```
df -h
lsblk
mount /dev/sdb1 /mnt/data
ls /mnt/data
```

Edit the block, save, quit, and Bash runs all of them in sequence, which is genuinely useful when you realize mid-session that a multi-step setup procedure worked and you want to clean it up into a proper script before the session ends.

**Note**: ***If `$EDITOR` is not set, `fc` falls back to `vi` on most systems, so set it in `~/.bashrc` with `export EDITOR=vim` or whatever you prefer***.

10\. HISTCONTROL Stop Duplicate Commands in Bash

Not a shortcut exactly, but it makes every other shortcut in this article more useful by keeping your history clean and searchable.

Add this to your `~/.bashrc`:

```
HISTCONTROL=ignoreboth
```
- `ignoredups` skips storing a command if it’s identical to the previous one, so mashing **Enter** on the same command 5 times doesn’t clog your history.
- `ignorespace` skips storing any command that starts with a space, which is useful for commands you want to run but never want saved (like those with inline passwords).
- `ignoreboth` enables both.

After editing `~/.bashrc`, apply the change:

```
source ~/.bashrc
```

If you see a syntax error message, check the line you added for stray characters. A clean reload produces no output at all.

***What HISTCONTROL settings does your team use? [Share your setup in the comments](#comments "Share Your HISTCONTROL Settings") or do you use `ignoreboth` or something else?***

##### Conclusion

You came in knowing that `sudo !!` exists and left with `!$`, `!*`, `^old^new`, `!string:p`, `fc`, `Ctrl+R`, `Alt+.`, `HISTCONTROL`, and a smarter up arrow.

That’s the full picture of how Bash’s history expansion system fits together, and each piece solves a specific pattern that would otherwise cost you a few seconds of retyping every single time.

Pick one shortcut from this article and make it your focus for the next week. `Ctrl+R` alone changes how fast you work at the terminal, and once that’s muscle memory, `!$` and `^old^new` take maybe two days each to stick.

***Have you already been using some of these, or did a few of them surprise you? Which one are you going to try first? [Tell us in the comments](#comments "Share Bash History Tricks") below*.**

***If this saved you from another round of arrow-key hunting, share it with your team or someone on your Slack is still retyping commands the long way***.

Get the **Learn Linux 7 Days Crash Course** free when you join 34,000+ Linux professionals reading every Thursday.

Check your email for a magic link to get started.