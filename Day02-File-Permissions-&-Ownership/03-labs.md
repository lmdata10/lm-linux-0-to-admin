## Day 02 Lab Challenge: Secure Application Setup

**Scenario:** Your team is deploying a new application. You need to set up the directory structure with proper security permissions before the deployment.

**Your Tasks:**

### 1. Create Application Structure
```
Create: /lm/30-days-of-linux/daily-labs/day2/app-deployment/

Inside it, create:
- scripts/         (for deployment scripts)
- configs/         (for configuration files)
- logs/            (for application logs)
- secrets/         (for sensitive data)
- public/          (for public assets)
``` 
### 2. Create Sample Files
```
In scripts/:     deploy.sh, backup.sh, monitor.sh
In configs/:     app.conf, database.conf
In secrets/:     api-keys.txt, db-password.txt
In logs/:        app.log, error.log
In public/:      index.html, style.css
```

### 3. Set Security Permissions

**Scripts** (need to be executable):
- All **.sh** files: `755`

**Configs** (readable by application, not writable by others):
- All **.conf** files: `644`

**Secrets** (owner only):
- All files in secrets/: `600`

**Logs** (writable by owner, readable by group):
- All **.log** files: `640`

**Public** (readable by everyone):
- All files in public/: `644`

### 4. Document Security Audit

Create: `/lm/30-days-of-linux/daily-labs/day02/security-audit.txt`

It should contain:
- Output of `ls -lR app-deployment/` (full permission tree)
- Count of executable files
- List of files with 600 permissions
- Your username and date

---

## Success Criteria:

Run this validation command:

```bash
cd /lm/30-days-of-linux/daily-labs/day02

# Check all permissions
ls -lR app-deployment/

# Verify executable scripts
find app-deployment/scripts/ -type f -perm -u+x

# Verify secrets are restricted
find app-deployment/secrets/ -type f -perm 600

# Show your audit report
cat security-audit.txt
```


## Day 02 Checkpoint Questions

1. What does `chmod 755` mean in terms of read, write, execute?
- Owner: read, write, execute (7)
- Group: read, execute (5)
- Others: read, execute (5)


2. Why should secret files (like API keys) have `600` permissions instead of `644`?
- 600 = only owner can read/write, no one else can access
- 644 = group and others can read the secrets (security risk)

3. What's the difference between `chmod +x` and `chmod u+x`?
- chmod +x = adds execute for ALL (user, group, others) → 755
- chmod u+x = adds execute for USER only (owner) → 744
---