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


## Wildcards and Optional Characters


## Metacharacters and Repititions


## Starts with/ ends with, groups, and either/ or


---
