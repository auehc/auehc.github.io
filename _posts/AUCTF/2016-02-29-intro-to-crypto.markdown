---
tagline:  "Introduction to Cryptography"
date:   2016-02-27
categories: archived
author: auctf
tags: crypto
---

This week, Jacob went over the bare basics of cryptography, some of the most common ciphering techniques (substitution ciphers), and went over most of [Over The Wire's][overthewire] Krypton challenges.

# Encoding vs Encryption vs Hashing vs Obfuscation

Encoding, Encryption, Hashing, and Obfuscation all have to do with transforming data. When encoding, you transform the data in order for a system to properly and safely consume it. Encoding can be easily reverse and examples include Base64, ASCII, and URL Encoding. In contrast, you use encryption to transform data in order to keep it secret from anyone that shouldn't be reading it. Usually encryption has to do with high level math and secret keys (like RSA, or AES), but can be as simple as a substitution cipher like Caesar. Hashing is transformation to ensure integrity and any hashing algorithm should ensure that the same input produces the same output, in order to make sure data is unchanged. Examples include MD5 and SHA256. Obfuscation is used, usually for code, to make something harder to understand. If you don't want someone to be able to read or change the code you wrote then you would use obfuscation.

## Krypton Writeups

In order to access Krypton you'll need an SSH Client (puTTy for windows, native on Linux) and some basic knowledge of the Linux command line. To ssh into the box, you'll need to connect to krypton.labs.overthewire.org with the username kryptonX where X is the level you're on. This is better explained on the [website][overthewire].

# Krypton 0

The 0th level gives you the string 'S1JZUFRPTklTR1JFQVQ=' and tells you that it is Base64 encoded, which is relatively easy to reverse. Just plug it into a [decoding website][base64decode] or the linux command line to get the password to krypton1.

	echo 'S1JZUFRPTklTR1JFQVQ=' | base64 --decode

Base63 takes an input, like the word 'Man', converts it to ASCII, then to binary, and converts it back to ASCII in different group sizes. So the word 'Man' would turn into the ASCII values, 77-97-110, which is the same as the binary values, 01001101, 01100001, 01101110. These are concatenated together and converted into integers in groups of six, 010011, 010110, 000101, 101110 which correspond to 19,22,5,46 or the letters 'TWFu' based on the base64 index table.

# Krypton 1

If you log into krypton 1 and follow the instructions to the second challenge you'll find a README file that says that krypton2 is encrypted using ROT13. ROT13 is a cipher that rotates all of the letters in a sequence by 13 letters, so A becomes N and so on. Letters later on wrap around the alphabet so Z would become M. So in order to translate the file we can use a website like [Rumkin][rumkin] or the linux command

	cat krypton2 | tr 'A-Za-z' 'N-ZA-Mn-za-m'

# Krypton 2

This challenge is similar to last time, except this time we aren't given a key (last time it was 13) which implies it is a Caesar Cipher, a more modular ROT13 cipher. Caesar cipher works in the same way except letters in a sequence are rotated by X amount, where X is a key (13 for ROT13). So with a key of 3, A would rotate to D, Y would rotate to B, etc. Plugging krypton3 into [Rumkin][rumkin] or [Quipqiup][quipqiup] is the easiest way to bruteforce this, since there are only 25 possible solutions. Otherwise you can use some for loop and tr trickery in bash.

# Krypton 3

In krypton3 we aren't given a key, instead we are given a few extra files that we can do something called frequency analysis on. Frequency analysis is counting how many of each letter is found in data, and mapping that to the english language frequency chart and seeing if something near English pops out. ![Frequency Analysis](/assets/crypto/FA.png)  
For this challenge, we can use a tool like [CryptoClub][cryptoclub] (which looks like a child's game) to map the letters and figure out which alphabet was used.

# Krypton 4 + 5

Krypton 4 and 5 use a Vigenere Cipher, which is similar to a Caesar cipher, but instead of using a number key, it uses another word as the key, like 'GOLD.' Now in order to encrypt text, you line the text up with the key and rotate based on the number values in the key, aka 'G' = 6 which would translate P to V.

	PROCEED MEETING AS AGREED
	GOLDGOL DGOLDGO LD GOLDGO
	VFZFKSO PKSELTU LV GUCHKR

For 4 and 5, we use the same process of Frequency Analysis as we did in step 3, but with a different website suited for Vigenere, [The Black Chamber][blackchamber]. For Krypton 4, plug in the text and select the key length of 6, which was given to us. Scroll down to the bottom and line up the charts so that the frequencies of the given text and the frequencies of english are approximately the same and try and find out the key. Once you have the key you can decipher the krypton4 file using [Rumkin][rumkin]. With krypon5 we aren't given a keylength, so we have to use the pattern analysis given to us by Black Chamber to figure it out. Try the most likely key lengths and then try frequency analysis at the bottom and see if anything english pops out.



[Slides](/assets/powerpoints/introcrypto.pptx)  
[Reference][reference]  

[overthewire]: http://overthewire.org/wargames/krypton/krypton0.html
[reference]: https://danielmiessler.com/study/encoding-encryption-hashing-obfuscation/#encoding
[base64decode]: https://www.base64decode.org/
[rumkin]: http://rumkin.com/tools/cipher/
[quipqiup]: Quipqiup
[cryptoclub]: http://www.cryptoclub.org/tools/cracksub_topframe.php
[blackchamber]: http://www.simonsingh.net/The_Black_Chamber/vigenere_cracking_tool.html