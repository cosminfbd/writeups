# Krypton Level 1 → Level 2

## Level Info
The password for level 2 is in the file ‘krypton2’. 
It is ‘encrypted’ using a simple rotation. 
It is also in non-standard ciphertext format. 
When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. 
This helps obfuscate any patterns. 
This file has kept the plain text word boundaries and carried them to the cipher text. 
Enjoy!

## Write-Up
```shell
krypton1@krypton:/krypton/krypton1$ ls -laF
total 16
drwxr-xr-x 2 root     root     4096 Oct 25 13:38 ./
drwxr-xr-x 9 root     root     4096 Oct 25 13:38 ../
-rw-r----- 1 krypton1 krypton1  882 Oct 25 13:38 README
-rw-r----- 1 krypton1 krypton1   26 Oct 25 13:38 krypton2

krypton1@krypton:/krypton/krypton1$ cat README
Welcome to Krypton!

This game is intended to give hands on experience with cryptography
and cryptanalysis.  The levels progress from classic ciphers, to modern,
easy to harder.

Although there are excellent public tools, like cryptool,to perform
the simple analysis, we strongly encourage you to try and do these
without them for now.  We will use them in later excercises.

** Please try these levels without cryptool first **


The first level is easy.  The password for level 2 is in the file 
'krypton2'.  It is 'encrypted' using a simple rotation called ROT13.  
It is also in non-standard ciphertext format.  When using alpha characters for
cipher text it is normal to group the letters into 5 letter clusters, 
regardless of word boundaries.  This helps obfuscate any patterns.

This file has kept the plain text word boundaries and carried them to
the cipher text.

Enjoy!

krypton1@krypton:/krypton/krypton1$ cat krypton2
YRIRY GJB CNFFJBEQ EBGGRA
```
Este un cifru ROT13 simplu. Folosim `tr`:
```shell
krypton1@krypton:/krypton/krypton1$ echo "YRIRY GJB CNFFJBEQ EBGGRA" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
LEVEL TWO PASSWORD ROTTEN
```
