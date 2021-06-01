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

Questions:
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

Questions:
* Match all of the following words: Cat, fat, hat, rat
    - `.at`

* Match all of the following words: Cat, cats
    - `[Cc]ats?`

* Match the following domain name: cat.xyz
    - `cat\.xyz`

* Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz
    -

* Match every 4-letter string that doesn't end in any letter from n to z
    - `...[^n-z]`

* Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)
    - 


## Metacharacters and Repititions


## Starts with/ ends with, groups, and either/ or


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
