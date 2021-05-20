# Encryption - Crypto 101

## Key Terms

**Ciphertext** -- the result of encrypting plaintext; encrypted data

**Cipher** -- a method of encrypting/decrypting data, most modern-day ciphers are *cryptographic*

**Plaintext** -- data before encryption, often text, but not always

**Encryption** -- transforming data into *ciphertext*, using a *cipher*

**Encoding** -- NOT a form of encryption, immediately reversible; see *Base64*

**Key** -- some info needed to correctly decrypt *ciphertext* to obtain *plaintext*

**Passphrase** -- separate from a *Key*, similar to a password; used to protect a *Key*

**Asymmetric encryption** -- uses different *Keys* to encrypt/decrypt

**Symmetric encryption** -- uses the same *Key* to encrypt/decrypt

**Brute Force** -- attacking cryptography by trying different passwords or different *Keys*

**Cryptanalysis** -- attacking cryptography by finding a weakness in the underlying maths

**Alice and Bob** -- common representation of `A` and `B` when discussing cryptography; see [Wikipedia link](https://en.wikipedia.org/wiki/Alice_and_Bob)


## Why is Encryption Important?

Cryptography is used everyday to:

* protect confidentiality
* ensure integrity
* ensure authenticity

ie: connecting to SSH, your client/server establish an encrypted *tunnel*, so no one can snoop

ie: connecting to a bank, there's a certificate that uses cryptography to prove that it is actually your bank

ie: downloading a file, you can use cryptography to check the *checksum* of the data

Sensitive Data follows standards for encryption, like [PCI-DSS](https://www.pcisecuritystandards.org/documents/PCI_DSS_for_Large_Organizations_v1.pdf)

**PCI-DSS** -- states that data should be encrypted both in storage, and while being transmitted


## Crucial Crypto Maths

The **Modulo** operator `%` -- used in pretty much every programming language, or has it available through a library

`X % Y` is the *Remainder*, when `X` is divided by `Y`

ie: `25 % 5` = 0

ie: `23 % 6` = 5

important to know that modulo is not reversible:

ie: `x % 5 = 4` , there are infinite valid values for `x`


## Types of Encryption

* **Symmetric encryption**
    - same key to encrypt and decrypt data
    - faster than asymmetric
    - uses smaller keys
    - examples:
        + DES -- 56 bits long (considered broken)
        + AES -- 128 or 256 bits long

* **Asymmetric encryption**
    - uses a pair of keys, 1 for encryption, and 1 for decryption
        + referred to as a *public key*, and a *private key*
        + data encrypted with the private key can be decrypted with the public key, and vice-versa
    - slower than symmetric
    - uses larger keys
    - examples:
        + RSA -- 2048 to 4096 bit keys
        + Elliptic Curve Cryptography


## RSA - Rivest Shamir Adleman

## Establishing Keys Using Asymmetric Cryptography

## Digital Signatures and Certificates

## SSH Authentication

- dl files here

## Explaining Diffie Hellman Key Exchange

## PGP, GPG, and AES

- dl files here

## The Future - Quantum Computers and Encryption


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
