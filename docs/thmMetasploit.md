# MetaSploit

Metasploit is an open-source pentesting *framework*, a collection of tested exploits, and auxiliary/post exploitation tools


## Initializing

Initializing the database:
```bash
msfdb init
```

Show Help Options:
```bash
msfconsole -h
```

Start Metasploit:
```bash
msfconsole
```

Don't forget *quiet* mode `-q` -- starts metasploit console without the banner

Checking connection to databse:
```
db_status
```

Metasploit 5 uses a `postgresql` database


## Basic Commands

`help` or `?` in the metasploit prompt shows a help menu

`search` finds various modules in metasploit -- one of the most common commands

`use` after searching a module sets it as *active*

`info` shows the info about the active module or a specified module

`connect` is a built-in NetCat-like function in metasploit

`banner` -- shows the ascii banner for metasploit

`set` -- sets a value for a variable

`setg` -- sets a value for a global variable

`get` -- shows the value of a variable

`unset` -- changes the value of a variable to null/no value

`spool` -- writes console output to a file as well as on screen

`save` -- stores settings/active datastores to a settings file


## Modules

Metasploit consists of 6 core modules

The `Exploit` module:
* most common module utilized
* holds all of the exploit codes

The `Payload` module:
* used hand-in-hand with `Exploit` module
* contains various bits of shellcode to execute following exploitation

The `Auxilliary` module:
* used in scanning and verification of exploitable machines
* not the same as actual exploitation

The `Post` module:
* provides capabilities for *looting* and *pivoting* after exploitation

The `Encoder` module:
* modifies 'appearance' of exploits
* helps in payload obfuscation to avoid signature detection

The `NOP` module:
* used in buffer overflow and ROP attacks

note: Not all modules are loaded by default, but the command `load` can be used to load in different modules


## Move that Shell! - Practical

Port Scanning without Nmap:
```
db_nmap -sV <Machine IP> 
```


## We're in, now what? -- Shell Stabilization, Host Enumeration, and PrivEsc


## Makin' Cisco Proud -- Enumerating the Network


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
