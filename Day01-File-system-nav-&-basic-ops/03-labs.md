## Day 01 Lab Challenge: New Server Audit

**Scenario:** You've been given access to a new production server. Your team lead needs a quick audit report before deploying applications.

**Assigned Tasks:**

1. **Create audit workspace**
   ```bash

   # Create directory: ~/30-days-of-linux/daily-labs/day01/
   sudo mkdir -p ./30-days-of-linux/daily-labs/day01/

   # Inside it, create subdirectories: system-info, logs-backup, findings
   mkdir -p 30-days-of-linux/{system-info,logs-backup,findings}
   ```

2. **System exploration**
   ```bash
   
   # Navigate to /var/log
   cd /var/log/

   find *.log | head -5          # quick check

   # Find the 5 most recently modified .log files
   
   ls -lht *.log | head -5 # 
   # Lists .log files in current dir, sorted by modif time (newest first), shows top 5

   sudo find . -name "*.log" -type f -printf '%Tm-%Td %TH:%TM %p\n' | sort -rn | head -5
   # Recursively finds all .log files in subdirectories, formats output as MM-DD HH:MM + path, sorts newest first, shows top 5.

   # Copy those 5 files to your logs-backup directory
   sudo cp $(sudo ls -t /var/log/*.log | head -5) /lm/30-days-of-linux/logs-backup

   ```


3. **Document findings**
   ```bash
   # Create a file: ~/30-days-of-linux/daily-labs/day01/audit-report.txt
   
   cd /lm/30-days-of-linux/daily/labs/day01
   touch audit-report.txt

   # It should contain:
   # - Your username (hint: whoami command)
   # - Your home directory path
   # - Current date and time
   # - List of the 5 log files you copied

   cat > audit-report.txt << EOF
   > Username: $(whoami)
   > Home Directory: $HOME
   > Current date and time: $(date)
   >
   > Log files copied:
   > $(ls /lm/30-days-of-linux/logs-backlog/)
   EOF
   ```

## What I Learned
Had permission issues writing to `audit-report.txt` the directory was owned by root. Fixed it by changing ownership:

`sudo chown -R lm-rocky:lm-rocky /lm/`

Tested both echo >> and heredoc (<< EOF) for adding content. Heredoc is cleaner for multi-line writes.

---

## Day 01 Checkpoint Questions

Answer these (don't look them up, test your understanding):

1. What's the difference between `cd ..` and `cd -`?
`cd ..` moves to the parent directory. `cd -` takes you to the last directory you were in.

2. How do you create nested directories in one command?
`mkdir -p /parent/child1/grandchild2`

3. What does `ls -ltr` do and why would an SRE use it?
Shows detailed file info sorted by modification time (oldest first). SREs use it to quickly find recent logs or track when files changed.

---