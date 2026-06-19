---
title: add SSH from Linux to GitHub
description: Generating SSH keys inside Linux WSL2 and then connecting Linux with the GitHub for Commit, Push, Pull etc...
aliases:
  - ssh-linux-github
---
**Option 1 — SSH Key (Recommended)**

1. Generate an SSH key inside WSL2:
```bash
ssh-keygen -t ed25519 -C "user_name@gmail.com"
```

Press Enter to accept defaults (no passphrase is fine for local dev).

2. Copy your public key:
```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output.

3. Add it to GitHub:
- Go to GitHub → Settings → SSH and GPG keys → New SSH key
- Paste your key and save.

4. Test the connection:
```bash
ssh -T git@github.com
```

You should see: Hi <username>! You've successfully authenticated...

5. Make sure your remote uses SSH (not HTTPS):
```bash
git remote -v
```

If it shows:  **https://github.com/...,** switch it to SSH:

```bash
git remote set-url origin git@github.com:<your-username>/<your-repo>.git
```
Now **git push** will work.


### what is this command? **ssh-keygen -t ed25519 -C "user_name@gmail.com"** and **ed25519**?

**ssh-keygen command breakdown**

```bash
ssh-keygen -t ed25519 -C "user_name@gmail.com"
```
┌────────────┬─────────────────────────────────────────────────────┐
│    Part            │                       Meaning                       │
├────────────┼─────────────────────────────────────────────────────┤
│ ssh-keygen │ tool that generates SSH key pairs                   │
├────────────┼─────────────────────────────────────────────────────┤
│ -t ed25519 │ type of encryption algorithm to use                 │
├────────────┼─────────────────────────────────────────────────────┤
│ -C "email" │ a comment/label to identify the key (just metadata) │
└────────────┴─────────────────────────────────────────────────────┘

### What is ED25519?

It is a **modern cryptographic algorithm** used to **generate SSH keys**. It creates a key pair:

- **~/.ssh/id_ed25519** — your **private key** (never share this)
- **~/.ssh/id_ed25519.pub** — your **public key** (you give this to GitHub)

When you push to GitHub:
1. GitHub sends a challenge encrypted with your public key
2. Only your private key can decrypt it
3. If it matches — you are authenticated, no password needed

---
### Why ED25519 and not something else?

There are **older algorithms** like **RSA and DSA**. **ED25519** is recommended because:

- Faster — smaller keys, quicker authentication
- More secure — harder to crack than older RSA-2048
- Simpler — fixed key size, less room for configuration mistakes

> **GitHub's own docs recommend ED25519 for all new SSH keys.**

---
In short: it generates a pair of math-linked keys — GitHub holds one, your machine holds the other — and together they prove your identity without a password.