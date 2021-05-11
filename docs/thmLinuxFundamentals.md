# Linux Fundamentals - TryHackMe Writeups

## Part 1

* Machine IP: 10.10.40.204

* login -- shiba1:shiba1

* **login2 found -- shiba2:pinguftw**

    1. creating noot.txt

    2. running shiba1 binary

```
touch noot.txt
./shiba1
```


## Part 2

* Machine IP: 10.10.164.222

* login2 -- shiba2:pinguftw

* [Download link for Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

* sytax for ssh:
```
pingu2@10.10.164.222
```

* Special Operators:
```text
&& -- and
& -- background process
$ -- denotes environmental variables
| -- pipe symbol
; -- similar to && but doesn't require succesful 1st command
> -- output redirect
>> -- similart to > but appends output instead of erasing
```

* $ uses:
```
echo $USER
touch $USER
```

* set an environmental variable
```
export nootnoot=1111
```

* print home directory
```
echo $HOME
```

* chown command -- change owner
```
chown shiba2:shiba2 file
```

* chmod -- file permissions
```
chmod <permissions> <file>
```

* rm -- remove
```
rm <directory>
rm -rf <directory>
```

* mv -- move; can also be used to rename files
```
mv <file> <destination>
```

* **login3 found -- shiba3:happynootnoises**

    1. setting $USER variable to test1234

    2. running shiba2 binary

```
export test1234=$USER
./shiba2
```


## Part 3

* Machine IP: 10.10.63.139

* login3 -- shiba3:happynootnoises


### Advanced File Operators

- cp -- duplicates aka copies
```
cp <file> <destination>
```

- cd -- change directory
```
cd <directory>
```

- mkdir -- make directory
```
mkdir <directory name>
```

- ln -- linking:
1. "hard linking" -- completely duplicates file
```
ln source destination
```
2. "symlinking" -- symbolic linking; glorified reference
    - shows arrow pointing to reference file
```
ln -s <file> <destination>
```

- find -- find files by listing every file in current directory
    - works recursively
    - only works on directories you have permissions to
```
find /tmp
find /
find dir -user
find dir -group
find -perm
find / user paradox
```

- grep -- find data inside data
    - can be piped
```
grep <regular expression> <file>
grep <string> <file>
grep <string> <file> <file2>
grep hello test -n
find /* | grep test1234
grep boop /tmp/aaaa
```

- **login4 found -- shiba4:test1234**

    1. used find/grep/less to locate shiba4 binary
        - /etc/shiba/shiba4
        - /opt/secret/shiba4
```
find /* | grep shiba4 | less
```

- sudo -- aka root aka administrator
```
sudo <command>
sudo -U jen whoami
```

### Users & Groups

- to add users -- must be sudo
```
adduser username
addgroup groupname
```

-  to add user to group
```
usermod -a -G <groups seperated by commas> <user>
usermod -a -G b noot
sudo usermod -a -G test test
```

- to view basic usesr info
```
id
```

### Intro to Shell Scripting

- .sh files store multi line commands

- shebang -- first line in code; indicates language of script
```bash
#!/bin/bash
```

- remove file extention and make executable
```bash
mv s.sh s
chmod 777 s
./s
```

### Important Files and Directories

- /etc/passwd 

    - stores user info 

    - used to see all users on a system

- /etc/shadow 

    - has all user passwords

- /tmp 

    - temporary files 

    - deleted on shutdown

- /etc/sudoers 

    - control sudo permissions

- /home 

    - windows equivalent:
```
C:\Users\<user>
```

- /root 

    - windows equivalent:
```
C:\Users\Administrator
```

- /usr 

    - where all your software is installed

- /bin and /sbin 

    - critical system files
 
- /var 

    - linux miscellaneous diectory

- $PATH 

    - stores binaries you're able to run

    - same as Windows

### Processes

- see "top" program for more info

- list user created processes
```
ps
```

- to list all running processes
```
ps -ef
```

- to kill a process
```
kill <PID>
```

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
