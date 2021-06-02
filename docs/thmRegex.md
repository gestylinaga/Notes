# Regular Expressions

**Regular Expressions** or **Regex** -- patterns of text that you define to search documents, and match exactly what you're looking for


## Charsets

Searching for a specific string in a file or block of text:
```bash
grep 'string' <file>
```

But, searching for a *pattern* of text requires **Charsets** -- find **every** occurance of the pattern defined

A charset is defined by:
* Square brackets -- `[ ]`
* the character(s), or range of characters you want to match

Examples:
`[abc]` will match `a`, `b`, and `c`

`[abc]zz` will match `azz`, `bzz`, and `czz`

`-` define ranges, so the above line would return the same results as: `[a-c]zz`

Ranges can also be combined:

`[a-cx-z]zz` will match `azz`, `bzz`, `czz`, `xzz`, `yzz`, and `zzz`

This can be used to match cases too:

`[a-zA-Z]` will match any **single** character

also works with numbers:

`file[1-3]` will match `file1`, `file2`, and `file3`

To **Exclude** characters from a charset, theres the `^` character:

`[^k]ing` will match `ring`, `sing`, and `$ing`, but not `king`

Which can also be used with ranges to exclude whole charsets

`[^a-c]at` will match `fat` and `hat`, but not `bat` or `cat`

Tasks:
* Match all of the following characters: c, o, g
    - `[cog]`

* Match all of the following words: cat, fat, hat
    - `[cfh]at`

* Match all of the following words: Cat, cat, Hat, hat
    - `[CcHh]at`

* Match all of the following filenames: File1, File2, file3, file4, file5, File7, file9
    - `[fF]ile[1-9]`

* Match all of the filenames of question 4, except "File7" (use the hat symbol)
    - `[fF]ile[^7]`


## Wildcards and Optional Characters

The wildcard that is used to match any single character is the `.` dot

That means that `a.c` will match `aac`, `abc`, `a0c`, `a!c`, etc...

The `?` question mark wildcard is used to set an *optional* pattern

so `abc?` will match `ab` and `abc`, since the `c` is optional

Note to search for a literal `.` dot, you have to *excape* it with a `\` reverse slash

so searching for `a\.c` will match **just** `a.c`

Tasks:
* Match all of the following words: Cat, fat, hat, rat
    - `.at`

* Match all of the following words: Cat, cats
    - `[Cc]ats?`

* Match the following domain name: cat.xyz
    - `cat\.xyz`

* Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz
    - `[ch]ats?\.xyz`

* Match every 4-letter string that doesn't end in any letter from n to z
    - `...[^n-z]`

* Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)
    - `[^r]ats?`


## Metacharacters and Repetitions

An easier way to match bigger charsets:
* `\d` matches a digit, like `9`
* `\D` matches a non-digit, like `A` or `@`
* `\w` matches an alphanumeric character, like `a` or `3`
* `\W` matches a non-alphanumeric character, like `!` or `#`
* `\s` matches a whitespace character, like spaces, tabs, and line breaks
* `\S` matches everything else (alphanumeric characters and symbols)

Note that `_` underscores are included in the `\w` metacharacter, and not in `\W`

**Repititions** are used to find patterns of many characters of a single type in a row

ie: `z{2}` will match exactly `zz`

For Reference:
* `{12}` -- exactly 12 times
* `{1,5}` -- 1 to 5 times
* `{2,}` -- 2 or more times
* `*` -- 0 or more times
* `+` -- 1 or more times

Tasks:
* Match the following word: catssss
    - `cats{4}`

* Match all of the following words (use the * sign): Cat, cats, catsss
    - `[Cc]ats*`

* Match all of the following sentences (use the + sign): regex go br, regex go brrrrrr
    - `regex go br+`

* Match all of the following filenames: ab0001, bb0000, abc1000, cba0110, c0000 (don't use a metacharacter)
    - `[abc]{1,3}[01]{4}`

* Match all of the following filenames: File01, File2, file12, File20, File99
    - `[Ff]ile\d{1,2}`

* Match all of the following folder names: kali tools, kali     tools
    - `kali\s+tools`

* Match all of the following filenames: notes~, stuff@, gtfob#, lmaoo!
    - `\w{5}\W`

* Match the string in quotes (use the * sign and the \s, \S metacharacters): "2f0h@f0j0%!     a)K!F49h!FFOK"
    - `\S*\s*\S*`

* Match every 9-character string (with letters, numbers, and symbols) that doesn't end in a "!" sign
    - `\S{8}[^!]`

* Match all of these filenames (use the + symbol): .bash_rc, .unnecessarily_long_filename, and note1
    - `\.?\w+`


## Starts with/ ends with, groups, and either/ or

`^` -- for patterns at the **beginning** of a line

`$` -- for patterns at the **end** of a line

ie: to search for a line that **starts with** `abc`, you can use `^abc`

ie: to search for a line that **ends with** `xyz`, you can use `xyz$`

Note that `^` and `[^]` are very different:
* `^` outside of brackets means *beginning of a word*
* `[^]` inside brackets means *exclude a charset*

`(`Parentheses`)` are used to define **Groups**
* can be used to define an either/or pattern
* `|` pipe symbol used as the *or* in regex

ie: the pattern `during the (day|night)` will match both `during the day` and `during the night`

ie: the pattern `(no){5}` will match the sentence `nonononono`

Tasks:
* Match every string that starts with "Password:" followed by any 10 characters excluding "0"
    - `^Password:[^0]{10}`

* Match "username: " in the beginning of a line (note the space!)
    - `^username:\s`

* Match every line that doesn't start with a digit (use a metacharacter)
    - `^\D`

* Match this string at the end of a line: EOF$
    - `EOF\$$`

* Match the following sentences: "I use nano", and "I use vim"
    - `I use (nano|vim)`

* Match all lines that start with $, followed by any single digit, followed by $, followed by one or more non-whitespace characters
    - `\$\d\$\S+`

* Match every possible IPv4 IP address (use metacharacters and groups)
    - `(\d{1,3}\.){3}\d{1,3}`

* Match all of these emails while also adding the username and the domain name (not the TLD) in separate groups (use \w): hello@tryhackme.com, username@domain.com, dummy_email@xyz.com
    - `(\w+)@(\w+)\.com`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
