# Guided Practice

Run these commands to get comfortable:

```bash
# 1. Explore the system
pwd
cd /
ls -l
cd /var/log
ls -lt | head -5
cd ~
pwd

# 2. Create test structure
mkdir -p ~/practice/logs
mkdir -p ~/practice/configs
cd ~/practice
touch file1.txt file2.txt
ls -l

# 3. Practice navigation
cd logs
pwd
cd ..
pwd
cd -
pwd

# 4. Copy and move
cp file1.txt logs/
ls logs/
mv file2.txt backup.txt
ls -l
```

---