# Guided Practice

Run this commands to get comfortable:

```bash
# 1. Create test environment
cd /lm/30-days-of-linux/daily-labs/day02
mkdir permission-lab
cd permission-lab

# 2. Create test files
touch script.sh config.conf secret.txt public.txt
ls -l

# 3. Practice viewing permissions
ls -l script.sh
ls -ld .

# 4. Make script executable
chmod +x script.sh
ls -l script.sh
# Notice the 'x' appears

# 5. Set proper permissions
chmod 755 script.sh      # Scripts should be executable
chmod 644 config.conf    # Config files readable by all
chmod 600 secret.txt     # Secrets only for owner
chmod 644 public.txt     # Public readable

# 6. Verify all permissions
ls -l

# 7. Test removing permissions
chmod -x script.sh       # Remove execute
ls -l script.sh
chmod +x script.sh       # Add it back

# 8. Practice with symbolic notation
chmod u+w,g-w,o-r secret.txt
ls -l secret.txt
```

---
