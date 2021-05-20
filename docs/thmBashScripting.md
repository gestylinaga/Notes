# Bash Scripting

What is *bash*?

**Bash** is a scripting language than runs in the terminal on most Linux distros, and MacOS

*Shell Scripts* are a sequence of bash commands within a file that together, achieve a complex task


## Bash Scripts Basics

The **Hashbang** or first line, for bash scripts:

- this lets your shell know to run the file in *bash*

```bash
#!/bin/bash
```

The `echo` command -- similar to `print` in Python
```bash
#!/bin/bash

echo "Hello World!"
```

You can also run normal Linux commands, like `ls`, inside a bash script
```bash
#!/bin/bash

echo "Hello World!"

whoami

id
```

Don't forget to make your scripts *executable*
```bash
sudo chmod +x scriptName.sh
```

then you can run it with `./`
```bash
./scriptName.sh
```


## Variables

```bash
name="Jammy"
```
In this example, the variable `name` is assigned the variable `Jammy` -- notice the lack of spaces

To call, add a `$`
```bash
name="Jammy"
echo $name


Jammy
```

### Debugging

Built-in bash debugger:
```bash
bash -x ./fileName.sh
```
- this retuturns a `+` on for valid command lines, and a `-` on lines with errors

Debugging inside a script:
```bash
echo "hi"

set -x

# this section will be debuggd

set +x
```


## Parameters
```bash
name=$1

echo $name
```

if run with:

```
./example.sh Alex
```

would return: `Alex`

For returning the 2nd argument:
```bash
name=$2

echo $name
```

running the above example:
```
./example2.sh Alex Tony
```
would return `Tony`

Or, there's the `read` command -- similar to `input` in Python
```bash
echo "Enter your name"

read name

echo "Your name is $name"
```


* `$#` -- shows the *number* of arguments supplied to a script

* `$0` --  shows the *filename* of the current script


## Arrays

**Arrays** are used to store multiple pieces of data in one variable.
They can then be extracted using an index.

```bash
var[index_position]
```
Remember, indexes start at position 0

```bash
['car', 'train', 'bike', 'bus']
```
therefore `car` would be item 0, `bike` would be item 2, etc...

Sample Syntax:
```bash
transport =('car' 'train' 'bike' 'bus')
```

and using echo to display the elements in the array:
```bash
echo "${transport[0]}"

car
```

To delete an element, use the `unset` utility:
```bash
unset transport[1]
```

To *set* the element as a new value:
```bash
transport[1]='trainride'
```


## Conditionals

determined with *relational* operators: `>`, `<`, and `=`

* `if` statements sample syntax:
    - `[ ]` with a space on both sides of the text
    - ending the `if` statement with an `fi`
    - the `-eq` can be substituted with a `=`

* Some example operators:
    - `-eq` -- equal =
    - `-ne` -- not equal !=
    - `-gt` -- greater than >
    - `-lt` -- less than <
    - `-ge` -- greater than or equal to >=

```bash
count=10

if [ $count -eq 10 ]

then

    echo "true"

else

    echo "false"

fi
```


---
## External Links

[Bash Scripting Cheatsheet](https://devhints.io/bash)

Suggested Further Reading:

- [CodeWars](https://www.codewars.com/)

- [HackerRank](https://www.hackerrank.com/)

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
