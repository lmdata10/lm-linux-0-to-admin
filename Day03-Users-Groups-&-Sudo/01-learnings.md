# Day 03: Users, Groups & Sudo

## Core Concepts

**Linux Multi-User Model:**
- Every file and process belongs to a specific user
- Users belong to one or more groups
- Root (UID 0) is the superuser with unrestricted access
- Regular users need `sudo` for privileged operations

**Why This Matters for SRE:**
- Web servers run as `www-data` or `nginx` (not root) for security
- You'll create service accounts for applications
- `sudo` logs all privileged commands (audit trail)
- Misconfigured sudo = security breach or broken deployments

**Key Files:**
```
/etc/passwd   - User account info
/etc/group    - Group definitions
/etc/shadow   - Encrypted passwords (root only)
/etc/sudoers  - Sudo permissions (edit with visudo)
```

---

## Command Reference

```bash
# USER MANAGEMENT
whoami                           # Show current user
id                               # Show user ID, group IDs
id username                      # Show info for specific user
groups                           # Lists all groups you belong to.

sudo useradd developer           # Create user (minimal setup)
sudo useradd -m -s /bin/bash dev # Create user with home dir + shell
sudo useradd -r user             # Create a system account
sudo userdel developer           # Delete user (keeps home dir)
sudo userdel -r developer        # Delete user + home directory

sudo passwd username             # Set/change user password
passwd                           # Change YOUR password

# GROUP MANAGEMENT
groups                           # Show groups you belong to
groups username                  # Show groups for specific user

sudo groupadd developers         # Create group
sudo groupdel developers         # Delete group

sudo usermod -aG groupname user  # Add user to group (append)
sudo usermod -g groupname user   # Change user's primary group
sudo gpasswd -d user group       # Remove user from group

# SWITCHING USERS
su - username                    # Switch to user (login shell)
su username                      # Switch to user (current environment)
sudo su -                        # Become root (login shell)
exit                             # Return to previous user

# SUDO
sudo command                     # Run command as root
sudo -u username command         # Run command as specific user
sudo -i                          # Get root shell (interactive)
sudo -l                          # List your sudo permissions
```

**User Creation Best Practice:**
```bash
# Application service account (no login)
sudo useradd -r -s /usr/sbin/nologin appuser

# Developer account (with home directory)
sudo useradd -m -s /bin/bash -G developers,docker alice
sudo passwd alice
```