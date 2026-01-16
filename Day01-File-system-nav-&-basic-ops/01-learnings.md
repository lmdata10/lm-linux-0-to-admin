# Day 01: File System Navigation & Basic Operations

## Core Concepts

**File System Hierarchy:**
- Everything starts from `/` (root directory)
- `/home` - user home directories
- `/etc` - system configuration files
- `/var` - variable data (logs, databases)
- `/tmp` - temporary files

**Path Types:**
- **Absolute path:** `/home/user/file.txt` (starts from root)
- **Relative path:** `../file.txt` (relative to current location)

**Special Directories:**
- `.` - current directory
- `..` - parent directory
- `~` - your home directory
- `-` - previous directory

---

## Command Reference

```bash
pwd                          # Print working directory
cd /path/to/directory        # Change directory (absolute)
cd ../                       # Go up one level
cd ~                         # Go to home directory
cd -                         # Go to previous directory

ls                           # List files
ls -l                        # Long format (permissions, size, date)
ls -la                       # Include hidden files
ls -lh                       # Human-readable sizes
ls -lt                       # Sort by time (newest first)
ls -ltr                      # Sort by time (oldest first)

mkdir project                # Create directory
mkdir -p project/src/config  # Create nested directories

touch file.txt               # Create empty file
cp source.txt dest.txt       # Copy file
cp -r folder/ backup/        # Copy directory recursively
mv old.txt new.txt           # Rename/move file
rm file.txt                  # Delete file
rm -r folder/                # Delete directory recursively
rm -i file.txt               # Interactive delete (asks confirmation)
```

---

