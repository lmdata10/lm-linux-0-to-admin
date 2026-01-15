# Lab - L2: Using Essential Tools

- ﻿﻿Use man and related resources to find out how to change the hostname of your computer
- ﻿﻿Read the help output for ip and find how you can bring down a link.
## Solution

```bash
man -k hostname
man hostnamectl
hostnamectl --help

# hostname [NAME]        Get/set system hostname

hostnamectl hostname rocky

################################################################

ip --help
ip link help
ip a
sudo ip link set enp2s0 down
ip a
sudo ip link set enp2s0 up
```

