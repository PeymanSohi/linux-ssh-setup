```markdown
# Linux SSH Setup Project

## 🧠 Project Goal
This project is designed to help me learn and practice the basics of Linux, specifically setting up a remote Linux server and configuring secure SSH access.

---

## 📋 Requirements
- Provision a remote Linux server (e.g., DigitalOcean, AWS, etc.)
- Create **two** new SSH key pairs
- Add both public keys to the server
- Successfully SSH into the server using both keys:
  ```bash
  ssh -i <path-to-private-key> user@server-ip
  ```
- Configure `~/.ssh/config` for easier access:
  ```bash
  ssh myserver
  ```

---

## 🚀 Steps Taken

### 1. Provisioned a Server
- Provider used: _e.g., DigitalOcean / AWS EC2_
- OS: _Ubuntu 22.04_

### 2. Created SSH Key Pairs
```bash
ssh-keygen -t ed25519 -f ~/.ssh/linux_key1
ssh-keygen -t ed25519 -f ~/.ssh/linux_key2
```

### 3. Added Public Keys to Server
Copied both `linux_key1.pub` and `linux_key2.pub` to `~/.ssh/authorized_keys` on the server:
```bash
ssh-copy-id -i ~/.ssh/linux_key1.pub user@server-ip
ssh-copy-id -i ~/.ssh/linux_key2.pub user@server-ip
```

### 4. Verified SSH Access
```bash
ssh -i ~/.ssh/linux_key1 user@server-ip
ssh -i ~/.ssh/linux_key2 user@server-ip
```

### 5. Configured SSH Alias
Content of `~/.ssh/config`:
```ini
Host myserver
    HostName <server-ip>
    User <user>
    IdentityFile ~/.ssh/linux_key1
```
Tested with:
```bash
ssh myserver
```

---

## 🎯 Stretch Goal: fail2ban Setup

### Installed fail2ban
```bash
sudo apt update
sudo apt install fail2ban -y
```

### Basic Configuration
Created a local jail config:
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```
Edited `/etc/fail2ban/jail.local` to ensure `sshd` jail is enabled:
```ini
[sshd]
enabled = true
```

### Restarted Service
```bash
sudo systemctl restart fail2ban
sudo systemctl status fail2ban
```

---

## ✅ Outcome
I am able to SSH into my server using both key pairs and an alias defined in `~/.ssh/config`.

---
https://roadmap.sh/projects/ssh-remote-server-setup
