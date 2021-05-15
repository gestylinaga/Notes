# Nmap -- Network Scanning Tool

* Target IP: 10.10.127.194

## 'Port' scanning

* **Ports** -- networking consruct that receives connections

    - allow for multiple network requests (think different tabs for different sites)

    - unique port for each individual webserver that connects

* every computer comes with **65535** available ports

    - many are registered as standard ports ie:

        - HTTP always on port 80

        - HTTPS always on port 443

        - Windows NETBIOS always on port 139

        - SMB always on port 445

* **Nmap** -- port scanner

    - Connects to each port in turn; port can respond:

        - Open

        - Closed

        - Filtered -- usually by firewall

    - Industry standard tool -- nothing else comes close in toolset


## Nmap Common Switches

- help
```
nmap -h
```

- Syn scan
```
nmap -sS
```

- UDP scan
```
nmap -sU
```

- Operating system
```
nmap -O
```

- services version
```
nmap -sV
```

- increase verbiosity
```
nmap -v
```

- level 2 verbiosity increase
```
nmap -vv
```

- save scan results in the 3 major formats
```
nmap -oA
```

- save to normal format 
```
nmap -oN
```

- save to 'grepable' format
```
nmap -oG
```

- Agressive mode -- service, OS, traceroute, scriptscanning...no need to be sneaky
```
nmap -A
```

- timing template at 5 (highest/loudest)
```
nmap -T5
```

- specific port scan
```
nmap -p 80
```

- scan all ports
```
nmap -p-
```

- activate a script from nmap scripting library
```
nmap --script
nmap --script=vuln
```

## Scan Types

* Most Common:

    - TCP Connect scans
    
    - SYN "half-open" scans

    - UDP scans

```
-sT
-sS
-sU
```

* Less common but important:

    - TCP Null Scans

    - TCP FIN scans

    - TCP Xmas scans

```
-sN
-sF
-sX
```


### TCP scans -- recall 3-way handshake in TCP protocols

* Nmap sends a **SYN** request to a port:

    - *closed* ports send back **RST** -- reset flag set

    - *open* ports send back **SYN/ACK** flag set

    - *firewalled* ports drop incoming packets, sending **nothing** back


### SYN scans 

* aka *half-open* or *stealth* scans

    - send back *RST* to target **after** *SYN/ACK* step

    - prevents server from making repeated connection requests

    - bypasses older intrusion detection systems

    - not logged by applications listening on open ports; because no full connection is made

* Disadvantages:

    - require sudo permisson

    - can bring down unstable services

* default scan if run with sudo permission; otherwise TCP scan


### UDP scans

- 'stateless'

    - instead of waiting for a "handshake", just sends packets and hopes for the best

    - speed over quality -- ie: video sharing

- packets sent to UDP ports should give no response

    - nmap refers to these as *open|filtered*

    - UDP ports that do send a response marked *open*

    - closed ports send ICMP (ping) packet back; marked as *closed*

- slower than the various TCP scans, useful commands to speed up:

```
--top-ports <number>
```

```
nmap -sU --top-ports 20 <target>
```
    
### NULL, FIN, and Xmas

* less common than other scans above; even *stealthier* than SYN scans

* **NULL** 

    - TCP request is sent with no flags set at all

    - target should respond with a RST if port is closed

* **FIN** 

    - similar to NULL, but sends FIN flag to gracefully close an active connection

    - same with NULL, target should respond with RST on closed ports

* **Xmas** 

    - sends malformed TCP packet

    - same as above; RST from closed ports

    - name comes from flags it sets in WireShark that look like a tree 

        - PSH

        - URG

        - FIN

* expected response from open ports are similar to UDP scans

    - only identify ports as: open|filtered, closed, or filtered

* Microsoft Windows and Cisco network devices are known to respond with RST to any malformed packet, whether open or not

    - results in all ports looking closed

* still useful for firewall evasion

    - many firewalls drop incoming TCP packets going to ports with SYU flag set

    - still not 100% effective


### ICMP Network Scanning

* ping sweep

    - nmap sends ICMP packets to each possible IP address, waiting for a response

```
nmap -sn 192.168.0.1-254
nmap -sn 192.168.0.1/254
```

* to ping sweep on the 172.16.x.x network (netmask 255.255.0.0) in CIDR notation

```
nmap -sn 172.16.0.0/16
```


## NSE Scripts

* **NSE** -- Nmap Scripting Engine

    - written in Lua programming language

    - can scan for vulnerabilities and automate exploits for them

    - Catergories:

        + safe -- won't affect target

        + intrusive -- not safe; likely to affect target

        + vuln -- scan for vulnerabilities

        + auth -- ateempt to bypass authentication (ie: logging into an FTP server anonymously)

        + brute -- attempt to bruteforce credentials

        + discovery -- attempt to query running services for more info about network

        + [complete list here](https://nmap.org/book/nse-usage.html)

* Usage

```
--script
--script=vuln
--script=safe
--script=<script-name>
--script=http-fileupload-exploiter
```

* Multiple scripts possible

```
--script=smb-enum-users,smb-enum-shares
```

* script arguments syntax

```
--script-args
```

* arguments separated by commas

```
--script=<script-name>,<argument>
```

* script help

```
nmap --script-help <script-name>
```

* for scripts help see:

    - [Nmap website](https://nmap.org/nsedoc/)

    - usr/share/nmap/scripts

    - usr/share/nmap/scripts/script.db

## Firewall Evasion

* tells nmap not to bother pinging before scanning

    - always treats host as alive; bypassing ICMP block

    - potentially takes longer to scan

```
-Pn
```

* to *fragment* packet -- smaller packets = harder to detect

```
-f
```

* alternative to -f; must be multiple of 8

```
--mt <number>
```

* delay time between sent packets

    - useful for unstable networks

```
--scan-delay <time>ms
```

* generates invalid checksums for packets

    - any real TCP/ICP stack would drop this, but some firewalls might not

```
--badsum
```

## Practical

1. pinged target; no response

```
ping 10.10.127.194
```

2. Xmas scan on first 999 ports; results in 999 open ports

    - show as all open because no responses from server (UDP scan)

```
sudo nmap -sX -Pn -p 0-998 10.10.127.194
```

3. TCP scan on first 5000 ports; 5 open

```
nmap -sT -Pn -vv -p 0-4999 10.10.127.194
```

4. using ftp-anon script on target; succesful login

```
nmap --script=ftp-anon 10.10.127.194
```

--- 
[back to TryHackMe main page](thm.md)

[back to Index/Table of contents](index.md)
