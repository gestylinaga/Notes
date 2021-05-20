# Cryptography for Dummies

Why is cryptography important?

Because without encryption, all communication across the internet would be entirely viewable/insecure


## Types of Cryptography

There are 2 types of cryptography: **Symmetric** and **Asymmetric**

Recall how *encryption* works:

* Alice *scrambles* a message with a *recipe* before sending it to Bob -- **Encryption**

* Bob has that same *recipe* and *unscrambles* the message -- **Decryption**

* The *recipe* in cryptography is the **Key**

In **Symmetric** cryptography, both users have the same key to encrypt/decrypt the message

In **Asymmetric** cryptography, the encryption and decryption key are different, making it more secure

* the *encryption* key is called the **Public Key**

* the *decryption* key is called the **Private Key**


## What is a Hash?

*Hashes* are long strings of letters and numbers genereated by hashing algorithms.

They take plain text and turn it into a *hash*.

Important to note that hashes are **not** reversible, there's no way to decrypt/decode a hash

Popular hashing algorithms:

* MD5 -- Message Digest 5

* SHA -- Secure Hash Algorithms

for example, `hello` in MD5 hash would be `5d41402abc4b2a76b9719d911017c592` 

Uses:

* file identification 

* storing sensitive data -- passwords: databases storing passwords as hashes

* ensuring data inregrity -- a MD5 hash will always produce the same output for the same input

example questions:

- `hashes are cool` in MD5: `f762d32e3c160900d94b683e927555b9`

- Who created MD5? -- Ronald Rivest


## Decoding/Encoding

There's a difference between *encoding* and *encrypting*

**Encrypted** files can only be decrypt with the key

**Encoded** data just needs to be *decoded*

Example of popular a encoding -- **Base64**:

- `hi there` -- `aGkgdGhlcmU=`

- `cryptographyisuseful` -- `Y3J5cHRvZ3JhcGh5aXN1c2VmdWw=`

- `dGhlIHNlY3JldCB3b3JkIGlzIDogd2F0ZXJtZWxvbg==` -- `the secret word is : watermelon`


---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
