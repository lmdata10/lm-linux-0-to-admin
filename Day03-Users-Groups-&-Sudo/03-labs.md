## Lab Challenge: Service Account Setup

**Scenario:** You're deploying a web application that needs:
- A dedicated user `webapp` (no login shell)
- A group `webadmin` for developers who manage it
- A directory `/var/www/myapp` owned by `webapp:webadmin` with proper permissions
- Your current user added to `webadmin` group

**Your Task:**
```bash
# 1. Create service account 'webapp' (no login)
sudo useradd -r -s /sbin/nologin webapp

# 2. Create 'webadmin' group
sudo groupadd webadmin

# 3. Add YOURSELF to webadmin (replace $USER with your name)
sudo usermod -aG webadmin $USER

# 4. Create app directory
sudo mkdir -p /var/www/myapp

# 5. Set ownership and permissions
#    - Owner: webapp, Group: webadmin
#    - Permissions: 770 (needed for directory access/traversal)
sudo chown -R webapp:webadmin /var/www/myapp
sudo chmod -R 770 /var/www/myapp

# 6. Verify setup
ls -ld /var/www/myapp
id webapp
```

---

## Day 3 Checkpoint Questions

**Answer these in your daily template. Paste them tomorrow.**

1. **What's the difference between `useradd -m` and `useradd -r`?**
- `useradd -m`  creates a user with home directory
- `useradd -r`  creates a system user with low UID, no home dir, to access services (web servers, apache, NGINX)

1. **Why would you create a service account with `/usr/sbin/nologin` as the shell?**
- It’s a security measure. It prevents anyone from logging into the account directly while still allowing the system to run services under that user, reducing the "attack surface" if the app is compromised.

1. **If you add yourself to a new group with `usermod -aG`, why do you need to log out and back in before the group membership takes effect?**
- Group permissions are only loaded when a new session starts. Your current shell won't recognize the new group until you re-authenticate (log out/in).


1. **What command shows you exactly which groups your current session has access to?**
- `groups`, `id`, `groups <username>` OR `groups $USERS`


5. **In the lab, why did we set `/var/www/myapp` to 770 instead of 777?**
- 770 limits access to the owner and group members only, whereas 777 allows any user on the system to modify or delete files.
- 777(NEVER) = security breach

