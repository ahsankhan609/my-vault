## Table Format vs. Subheading Format

==Use a table format when:== you have ==3+ commands under a heading== and you want to compare them side-by-side or quickly scan multiple options. Tables give you that bird's-eye view you mentioned—essential for reference work.

==Use subheadings when:== you need to ==explain _why_ a command works==, show _multi-step workflows_, or include code blocks and examples that don't fit neatly in table cells.

---
## User Management

| ==Command== | ==Syntax==                   | ==Example==       | ==Notes==                   |
| ----------- | ---------------------------- | ----------------- | --------------------------- |
| `useradd`   | `useradd [options] username` | `useradd john`    | Add `-m` to create home dir |
| `userdel`   | `userdel [options] username` | `userdel -r john` | Use `-r` to remove home dir |
### Why useradd vs adduser?
`useradd` is the low-level tool. `adduser` is a wrapper...

---
## File Management

| Command | Syntax                 | Example             | Notes                                                                         |
| ------- | ---------------------- | ------------------- | ----------------------------------------------------------------------------- |
| `ls`    | `ls [options] [path]`  | `ls -lah /home`     | list all files(hidden) with details, on terminal in the human readable format |
| `cp`    | `cp [source] [dest]`   | `cp file.txt /tmp/` | copy a file from ==current destination to another==                           |
| `mv`    | `mv old.txt new.txt`   |                     | Move or rename files                                                          |
| `rm`    | `rm file`              |                     | Delete files (irreversible)                                                   |
| `rm`    | `rm -rf folder/`       |                     | Delete File/Folder                                                            |
| `find`  | `find / -name "*.log"` |                     | search all files with `log` extension                                         |
| `chmdo` | `chmod 755 file`       |                     | Chnage Permission                                                             |
### Understanding Permissions with `chmod`
When you run `chmod 755 file`:- **7** (owner): read, write, execute- **5** (group): read, execute- **5** (others): read, execute

---
