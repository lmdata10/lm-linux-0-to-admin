
## Guided Practice

### Exercise 1: Create a User & Set Password
```bash
# 1. Create user 'testuser' with home directory
sudo useradd -m -s /bin/bash testuser

# 2. Set password
sudo passwd testuser
# (Enter password twice)

# 3. Verify user exists
id testuser
grep testuser /etc/passwd

# 4. Check home directory was created
ls -ld /home/testuser
```

---

### Exercise 2: Create Groups & Add Users
```bash
# 1. Create 'devteam' group
sudo groupadd devteam

# 2. Add testuser to devteam
sudo usermod -aG devteam testuser
# -a = append (keep her in her original groups too)
# cd-G = add to this secondary group


# 3. Verify
groups testuser
id testuser

# 4. Create a shared directory for the team
sudo mkdir -p de/shared/devteam
sudo chgrp devteam /shared/devteam          # change the group ownership of the directory to devteam
sudo chmod 770 /shared/devteam              # gives owner and group full access (rwx) and no permissions to others

# 5. Check permissions
ls -ld /shared/devteam
```

---

### Exercise 3: Sudo Permissions
```bash
# 1. Try running a privileged command as regular user
apt update          # Debian based. Ubuntu
dnf update          # RHEL based. Rocky
# (Should fail: Permission denied)

# 2. Run with sudo
sudo apt update

# 3. Check your sudo permissions
sudo -l

# 4. Check sudo logs
sudo journalctl -u sudo | tail -20
# Or on some systems:
sudo cat /var/log/auth.log | grep sudo | tail -20
```

---