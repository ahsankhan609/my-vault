# 👤 User Management

> [!info] About This Note
> Linux میں users اور groups کو manage کرنے کے لیے commands کا complete reference۔

**Tags:** #linux #user-management #sysadmin  
**OS:** Ubuntu / Debian / RHEL / Arch  
**Last Updated:** 2026-05-28

---

## 🗂️ Quick Reference Table

### 👦 User Commands

| Command | Example | Description |
|---------|---------|-------------|
| `useradd` | `useradd john` | نیا user بنائیں |
| `userdel` | `userdel john` | user کو delete کریں |
| `usermod` | `usermod -aG sudo john` | user کو modify کریں |
| `passwd` | `passwd john` | password set یا change کریں |
| `whoami` | `whoami` | current logged-in user دیکھیں |
| `id` | `id john` | user کی UID, GID اور groups دیکھیں |
| `w` | `w` | کون کون logged in ہے دیکھیں |
| `who` | `who` | logged-in users کی list |
| `last` | `last john` | user کی login history دیکھیں |
| `su` | `su - john` | دوسرے user میں switch کریں |
| `sudo` | `sudo apt update` | root permission سے command چلائیں |

### 👥 Group Commands

| Command | Example | Description |
|---------|---------|-------------|
| `groupadd` | `groupadd developers` | نیا group بنائیں |
| `groupdel` | `groupdel developers` | group کو delete کریں |
| `groupmod` | `groupmod -n dev developers` | group کا نام بدلیں |
| `groups` | `groups john` | user کے groups دیکھیں |
| `gpasswd` | `gpasswd -a john developers` | user کو group میں add کریں |
| `newgrp` | `newgrp developers` | active group change کریں |

### 📄 Important Files

| File | Description |
|------|-------------|
| `/etc/passwd` | تمام users کی info |
| `/etc/shadow` | encrypted passwords |
| `/etc/group` | تمام groups کی info |
| `/etc/sudoers` | sudo permissions |
| `/home/username/` | user کی home directory |

---

## 🔍 Detailed Command Reference

---

### `useradd` — نیا User بنانا

> نیا system user create کرتا ہے

**Syntax:**
```bash
useradd [options] username
```

**Examples:**
```bash
# Simple user بنائیں
useradd john

# Home directory کے ساتھ user بنائیں (recommended)
useradd -m john

# Custom home directory کے ساتھ
useradd -m -d /custom/home/john john

# Shell specify کریں
useradd -m -s /bin/bash john

# Group assign کریں
useradd -m -g developers john

# Multiple groups کے ساتھ (primary + secondary)
useradd -m -g developers -G sudo,docker john

# سب کچھ ایک ساتھ (production-ready command)
useradd -m -s /bin/bash -g developers -G sudo -c "John Doe" john
```

**Common Flags:**

| Flag | Full Form | کام |
|------|-----------|-----|
| `-m` | `--create-home` | home directory بنائے |
| `-d` | `--home-dir` | custom home path |
| `-s` | `--shell` | login shell set کرے |
| `-g` | `--gid` | primary group |
| `-G` | `--groups` | secondary groups |
| `-c` | `--comment` | full name یا description |
| `-r` | `--system` | system user بنائے (no home) |
| `-e` | `--expiredate` | account expire date |

> [!tip] 💡 Best Practice
> ہمیشہ `-m` flag لگائیں تاکہ home directory بھی بنے۔ بغیر `-m` کے home directory نہیں بنتی۔

> [!warning] ⚠️ یاد رہے
> `useradd` صرف user بناتا ہے — password الگ سے `passwd` سے set کرنا پڑتا ہے!

---

### `passwd` — Password Set کرنا

> User کا password set یا change کرتا ہے

**Syntax:**
```bash
passwd [options] [username]
```

**Examples:**
```bash
# اپنا password change کریں
passwd

# کسی اور user کا password set کریں (root only)
passwd john

# password expire کریں (اگلی login پر change کرنا پڑے گا)
passwd -e john

# password lock کریں
passwd -l john

# password unlock کریں
passwd -u john

# password کی expiry info دیکھیں
passwd -S john
```

**Common Flags:**

| Flag | کام                                      |
| ---- | ---------------------------------------- |
| `-e` | password فوری expire کرے                 |
| `-l` | account lock کرے                         |
| `-u` | account unlock کرے                       |
| `-d` | password delete کرے (passwordless login) |
| `-S` | password status دیکھے                    |

> [!warning] ⚠️ Security
> `-d` flag سے password ہٹانا بہت insecure ہے — production پر کبھی مت کریں!

---

### `usermod` — Existing User کو Modify کرنا

> پہلے سے موجود user کی settings بدلتا ہے

**Syntax:**
```bash
usermod [options] username
```

**Examples:**
```bash
# user کو sudo group میں add کریں
usermod -aG sudo john

# user کو docker group میں add کریں
usermod -aG docker john

# ایک ساتھ multiple groups میں add کریں
usermod -aG sudo,docker,developers john

# username بدلیں
usermod -l newname john

# home directory بدلیں
usermod -d /new/home/john john

# shell بدلیں
usermod -s /bin/zsh john

# account lock کریں
usermod -L john

# account unlock کریں
usermod -U john

# account expire date set کریں
usermod -e 2026-12-31 john
```

> [!danger] 🚨 بہت ضروری
> گروپ add کرتے وقت `-aG` استعمال کریں، صرف `-G` نہیں!
> صرف `-G` سے پرانے **سب groups ہٹ جاتے ہیں** اور صرف نیا group رہتا ہے۔
> `-a` کا مطلب ہے **append** — یعنی پرانے groups رہیں گے۔

---

### `userdel` — User Delete کرنا

> System سے user کو remove کرتا ہے

**Syntax:**
```bash
userdel [options] username
```

**Examples:**
```bash
# صرف user delete کریں (home directory رہے گی)
userdel john

# user اور home directory دونوں delete کریں
userdel -r john

# force delete (اگر user logged in ہو)
userdel -f john

# user + home + mail spool سب delete کریں
userdel -r -f john
```

> [!danger] 🚨 خطرناک Command
> `userdel -r` سے home directory مستقل delete ہو جاتی ہے — پہلے backup لیں!

---

### `id` — User Info دیکھنا

> User کی UID, GID اور تمام groups دکھاتا ہے

**Examples:**
```bash
# اپنی info دیکھیں
id

# کسی اور user کی info دیکھیں
id john

# صرف UID دیکھیں
id -u john

# صرف GID دیکھیں
id -g john

# صرف groups دیکھیں
id -G john

# groups بنام دیکھیں
id -Gn john
```

**Sample Output:**
```
uid=1001(john) gid=1001(john) groups=1001(john),27(sudo),998(docker)
```

---

### `sudo` اور `su` — Permission Switch کرنا

**`su` — User Switch:**
```bash
# دوسرے user میں switch کریں
su john

# environment بھی switch کریں (recommended)
su - john

# root میں جائیں
su -

# root کے طور پر ایک command چلائیں
su -c "apt update" root
```

**`sudo` — Root Permission سے Command چلانا:**
```bash
# root permission سے command چلائیں
sudo apt update

# root shell کھولیں
sudo -i

# دوسرے user کے طور پر command چلائیں
sudo -u john ls /home/john

# sudo cache clear کریں
sudo -k

# اپنی sudo permissions دیکھیں
sudo -l
```

> [!tip] 💡 `su` vs `sudo`
> - `su -` : پوری root shell — سب کچھ root کے طور پر
> - `sudo` : صرف ایک command root کے طور پر — زیادہ safe اور traceable

---

## 🔄 Common Workflows

### ✅ نیا User بنانے کا مکمل Workflow

```bash
# Step 1: User بنائیں
sudo useradd -m -s /bin/bash -c "John Doe" john

# Step 2: Password set کریں
sudo passwd john

# Step 3: sudo group میں add کریں (اگر admin ہو)
sudo usermod -aG sudo john

# Step 4: verify کریں
id john
grep john /etc/passwd
```

### ✅ User کو Delete کرنے سے پہلے

```bash
# Step 1: پہلے check کریں user logged in تو نہیں
who | grep john
w | grep john

# Step 2: home directory کا backup لیں
sudo tar -czf /backup/john_backup.tar.gz /home/john

# Step 3: اب delete کریں
sudo userdel -r john

# Step 4: verify کریں
id john  # "no such user" آنا چاہیے
```

### ✅ User کو Group میں Add کرنا اور Verify کرنا

```bash
# Add کریں
sudo usermod -aG docker john

# Verify کریں
groups john
id john

# نوٹ: changes اگلی login پر apply ہوں گے
# فوری apply کے لیے:
su - john   # یا logout/login
```

---

## 📝 Quick Notes

> [!note] UID Ranges (Linux Standard)
> - `0` → root
> - `1–999` → system users (services)
> - `1000+` → regular users

> [!note] `/etc/passwd` Format
> ```
> username:x:UID:GID:comment:home_dir:shell
> john:x:1001:1001:John Doe:/home/john:/bin/bash
> ```

> [!note] `/etc/shadow` Format
> ```
> username:hashed_password:last_changed:min:max:warn:inactive:expire
> ```

---

*🔗 Related Notes: [[File Management]] | [[Permissions & chmod]] | [[../Secure Shell (SSH) & Remote Access]]*
