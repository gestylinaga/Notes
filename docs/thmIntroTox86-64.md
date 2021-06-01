# Intro to x86-64

## Description and Objectives

This room looks at the basics of Intel's x86-64 assembly language

the tasks use the r2 reverse engineering framework -- [github link](https://github.com/radare/radare2)

Things to Note:
* this room uses AT&T syntax, not Intel syntax -- [see differences here](http://web.mit.edu/rhel-doc/3/rhel-as-en-3/i386-syntax.html)
* more radare2 docs [here](https://github.com/radare/radare2/blob/master/doc/intro.md), [here](https://gist.github.com/williballenthin/6857590dab3e2a6559d7), and [here](https://web.archive.org/web/20180312191821/http://www.radare.org/get/THC2018.pdf)
* remember to enter `e asm.syntax=att` to ensure you're using AT&T syntax when you start r2

## Introduction

Computers execute **Machine Code**, which is encoded as bytes, to carry out computer tasks

Machine code is usually represented in a more redable form of the code, called **Assembly Code**

Machine code is usually produced by a *compiler*, which takes the source code of a 
file, and after going through some intermediate stages, produces machine code that can be executed
by a computer

Intel started out with a 16-bit instruction set, followed by 32-bit, and finally 64-bit (which 
are all backwards compatible)

Before an executable file is produced:
* the source code is compiled into assembly -- .s files
* the assembler converts it into an object program -- .o files
* operations with a linker finally make it an executable

radare2 -- a framework for reverse engineering/analysing binaries
* used to *disassemble* binaries -- translate machine code to assembly, which is actually readable
* also used to debug said binaries -- by allowing a user to step through and view the state of the program


## If Statements


## If Statements Continued


## Loops


## crackme1


## crackme2



---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
