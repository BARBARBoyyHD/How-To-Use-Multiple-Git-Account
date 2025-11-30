Sure — here is a **clean, beginner-friendly README** that teaches you how to use **two Git accounts (personal GitHub + work GitLab)** on one computer using SSH aliases.

Use this as your personal guide.

---

# 🚀 Using Multiple Git Accounts (GitHub Personal + Work GitLab) on One Device

This guide explains how to:

* use different SSH keys
* switch between accounts automatically
* push/pull to the correct remote
* avoid authentication errors

Works for **Windows Git Bash**, macOS, and Linux.

---

# 📌 1. Create Your SSH Keys

### Personal GitHub key:

```
ssh-keygen -t ed25519 -C "personal email"
# save as: ~/.ssh/id_personal
```

### Work GitLab key:

```
ssh-keygen -t ed25519 -C "work email"
# save as: ~/.ssh/id_work
```

Your `~/.ssh` folder should contain:

```
id_personal
id_personal.pub
id_work
id_work.pub
config
```

---

# 📌 2. Add SSH Keys to GitHub & GitLab

### GitHub Personal

Go to: **GitHub → Settings → SSH & GPG Keys → Add New Key**

Paste the content of:

```
~/.ssh/id_personal.pub
```

---

### GitLab Work

Go to: **GitLab → Preferences → SSH Keys**

Paste:

```
~/.ssh/id_work.pub
```

---

# 📌 3. Configure SSH Aliases

Create or edit:

```
~/.ssh/config
```

Add this:

```
# Personal GitHub
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_personal

# Work GitLab
Host gitlab-work
    HostName git.gits.id
    User git
    IdentityFile ~/.ssh/id_work
```

This allows Git to automatically pick the right key.

---

# 📌 4. Cloning Repositories

### Personal GitHub

```
git clone git@github-personal:USERNAME/REPO.git
```

### Work GitLab

```
git clone git@gitlab-work:GROUP/PROJECT.git
```

---

# 📌 5. Creating a New Project & Pushing

### Initialize repo:

```
git init
git add .
git commit -m "initial commit"
```

### Add the correct remote:

#### Personal GitHub:

```
git remote add origin git@github-personal:USERNAME/REPO.git
```

#### Work GitLab:

```
git remote add origin git@gitlab-work:GROUP/PROJECT.git
```

### Push:

```
git branch -M main
git push -u origin main
```

---

# 📌 6. Check Your Current Remote

```
git remote -v
```

Expected examples:

### GitHub Personal:

```
origin  git@github-personal:BARBARBoyyHD/my-project.git
```

### Work GitLab:

```
origin  git@gitlab-work:nahrul/work-project.git
```

---

# 📌 7. Switching Between Accounts

You don’t need to change anything.

Git **automatically** chooses the right SSH key based on the host:

* `github-personal` → uses `id_personal`
* `gitlab-work` → uses `id_work`

Just push normally:

```
git push
git pull
```

---

# 📌 8. Testing Everything

### Test GitHub Personal:

```
ssh -T github-personal
```

### Test Work GitLab:

```
ssh -T gitlab-work
```

You should see:

```
Hi <username>! You've successfully authenticated!
Welcome to GitLab, @yourusername!
```

---

# 📌 9. Common Errors & Fixes

### ❌ `Permission denied (publickey)`

Your remote URL is wrong.

Fix:

```
git remote set-url origin git@github-personal:USER/REPO.git
```

or:

```
git remote set-url origin git@gitlab-work:GROUP/PROJECT.git
```

---

### ❌ `src refspec main does not match any`

No commit yet.

Fix:

```
git add .
git commit -m "initial commit"
git branch -M main
git push -u origin main
```

---

### ❌ Host not found

You opened **Windows CMD or PowerShell**.
Use **Git Bash** instead.

---

# 🎉 Done!

You can now smoothly use:

* **Personal GitHub projects**
* **Work GitLab projects**
* both on the same machine
* without conflicts
* without logging in/out

---


