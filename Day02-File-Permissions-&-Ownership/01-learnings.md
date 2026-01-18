# Day 02: File Permissions & Ownership

## Core Concepts

**Linux Permission Model:**
Every file/directory has:
- **Owner** (user who created it)
- **Group** (group of users)
- **Others** (everyone else)

**Permission Types:**
- `r` (read) = 4
- `w` (write) = 2  
- `x` (execute) = 1

**Permission Format:**
```
-rwxr-xr--
│└┬┘└┬┘└┬┘
│ │  │  └─ Others: r-- (read only) = 4
│ │  └──── Group: r-x (read, execute) = 5
│ └─────── Owner: rwx (read, write, execute) = 7
└──────── File type (- = file, d = directory)
```

**Why This Matters for SRE:**
- Scripts need execute permission to run
- Log files should be readable but not writable by others
- Config files often need restricted permissions (600, 644)
- Wrong permissions = security vulnerabilities or broken applications

---

## Command Reference

```bash
# VIEW PERMISSIONS
ls -l file.txt                    # Show permissions
ls -ld directory/                 # Show directory permissions

# CHANGE PERMISSIONS (chmod)
chmod 755 script.sh               # rwxr-xr-x (owner full, others read+execute)
chmod 644 config.txt              # rw-r--r-- (owner read+write, others read)
chmod 600 secret.txt              # rw------- (owner only)
chmod +x script.sh                # Add execute permission for all
chmod u+x script.sh               # Add execute for user (owner) only
chmod g-w file.txt                # Remove write permission from group
chmod o-r file.txt                # Remove read permission from others
chmod a+rwx filename              # Add read, write, and execute permissions to all (user, group, other)
chmod u=rwx,g=rw,o=r file.txt     # Set explicit permissions: user=rwx, group=rw, other=r
chmod 755 /path/to/dir            # Change permissions of directory only (not contents)
chmod -R 755 /path/to/dir         # Recursively change directory + all subdirs and files inside it
chmod 755 /path/to/dir/*          # Change permissions of all items within directory only. Does NOT change the dir itself
chmod -R u=rwx,g=rx,o=rx /path    # Better recursive approach: explicit permissions. Use this instead of blindly applying 755 everywhere


# CHANGE OWNERSHIP (chown)
sudo chown user file.txt          # Change owner
sudo chown user:group file.txt    # Change owner and group
sudo chown -R user:group folder/  # Recursive (all files inside)

# CHANGE GROUP (chgrp)
sudo chgrp developers file.txt    # Change group only
```

**Common Permission Patterns:**
```
755 - Executable scripts, directories
644 - Regular files, config files (non-sensitive)
600 - Sensitive files (passwords, SSH keys)
777 - NEVER USE (security risk - everyone can do everything)
```

---