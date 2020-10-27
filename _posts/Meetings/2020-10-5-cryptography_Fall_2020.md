---
title:  "Cryptography Fall 2020"
permalink: /meetings/Crypto_Fall_2020
tags: meetings
author: therealjman
---

For the first week of October, we discussed cryptography and encoding.

# Topics

## (not quite) Encryption

### Encoding

The primary purpose of encoding is to change the form of data so it can be more easily processed by a certain system. Encoding is not a good form of encryption, as it can be easily decoded. Some examples of popular encoding methods include hexadecimal encoding, Base64 encoding, and even something like Morse Code.

### Obfuscation

Obfuscation is another method commonly confused with encryption, but it is a different method. Obfuscation is simply the act of making information more difficult to understand, typically used to hide source code. Usually it is possible to deobfuscate something, but depending on how much the information was obscured, it could take a lot of time.

### Hashing

Hashing algorithms usually take in a plaintext input and output a computed combination of hexadecimal numbers, commonly known as a hash. When the same input is passed into a hashing algorithm, it always produces the same output. Additionally, hashes cannot be reversed, it is not possible to go from the hash back to plaintext. Sometimes hashing algorithms use a salt, which is a piece of random data that is used as an additional input. Salted hashes can be used to encrypt passwords.

## Encryption

Encryption is simply the act of taking a message and making it hard to read so someone cannot easily intercept and read it. Encryption is done by using certain algorithms known as ciphers and using special keys to decrypt those ciphers. There are two main types of ciphers, symmetric and asymmetric ciphers. Symmetric ciphers use the same key for both encrypting and decrypting data. Asymmetric ciphers use two different keys, a public key to encrypt the message that is available to the public, and a private key that is kept secret to decrypt the message.

## Vingenere Cipher

The Vingenere cipher is a type of simple symmetric cipher. It works by shifting the letters in a message by using a key, similar to Caesar cipher. However, it is different from a Caesar cipher because it is much more difficult to decrypt without the key.

## RSA Cipher

The RSA cipher is an asymmetric cipher that is widely used to encrypt data. It works by having a public encryption key and a private decryption key. The encryption key is available to everyone and is derived from two large prime numbers that are kept secret, and then those numbers are used to create the secret decryption key.

## AES Encryption

AES encryption is a symmetric cipher that has become one of the leading encryption algorithms used today. AES uses three different key lengths, so it is very difficult to bruteforce. The encryption method it uses is fairly complex. First, the plaintext and first key are loaded into blocks. Then round keys are generated from the key schedule, and then the plaintext is XORed with the key. Then bytes are replaced according to a lookup table, the rows in the table are shifted, the columns are mixed, and then this sequence is repeated a certain number of times.

## Diffie Hellman Key Exchange

Diffie Hellman Key Exchange is a method of securely exchanging cryptographic keys over a public channel. It is a symmetric cipher, as it uses the discrete logarithm problem to establish the shared key and allow for faster encryption time. Diffie Hellman allows for other algorithms like AES to be secure as it allows the keys to be exchanged securely.

## Substitution & XOR Ciphers

The substitution cipher is a very simple and common cipher. It works by simply substituting letters for certain other letters or symbols. These are usually very easily decoded once the substitution method is known. The XOR cipher is another common cipher, commonly used in other encryption methods, such as AES. This cipher just XOR’s a message with a key to obtain the ciphertext

# Slideshow
<iframe src="//docs.google.com/gview?url=http://auehc.github.io/assets/powerpoints/Cryptography.pptx&embedded=true" style="width:600px; height:500px;" frameborder="0"></iframe>
