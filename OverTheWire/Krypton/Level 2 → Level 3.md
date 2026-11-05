# Krypton Level 2 → Level 3

## Level Info

ROT13 is a simple substitution cipher.

Substitution ciphers are a simple replacement algorithm. In this example of a substitution cipher, we will explore a ‘monoalphebetic’ cipher. Monoalphebetic means, literally, “one alphabet” and you will see why.

This level contains an old form of cipher called a ‘Caesar Cipher’. A Caesar cipher shifts the alphabet by a set number. For example:

```
plain:  a b c d e f g h i j k ...
cipher: G H I J K L M N O P Q ...
```

In this example, the letter ‘a’ in plaintext is replaced by a ‘G’ in the ciphertext so, for example, the plaintext ‘bad’ becomes ‘HGJ’ in ciphertext.

The password for level 3 is in the file krypton3. It is in 5 letter group ciphertext. It is encrypted with a Caesar Cipher. Without any further information, this cipher text may be difficult to break. You do not have direct access to the key, however you do have access to a program that will encrypt anything you wish to give it using the key. If you think logically, this is completely easy.

One shot can solve it!

Have fun.

Additional Information:

The encrypt binary will look for the keyfile in your current working directory. Therefore, it might be best to create a working direcory in /tmp and in there a link to the keyfile. As the encrypt binary runs setuid krypton3, you also need to give krypton3 access to your working directory.

Here is an example:

```shell
krypton2@melinda:~$ mktemp -d
/tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:~$ cd /tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ln -s /krypton/krypton2/keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ chmod 777 .
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ /krypton/krypton2/encrypt /etc/issue
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
ciphertext  keyfile.dat
```
## Write-Up

```shell
krypton2@krypton:/krypton/krypton2$ ls -laF
total 36
drwxr-xr-x 2 root     root      4096 Oct 25 13:38 ./
drwxr-xr-x 9 root     root      4096 Oct 25 13:38 ../
-rw-r----- 1 krypton2 krypton2  1815 Oct 25 13:38 README
-rwsr-x--- 1 krypton3 krypton2 16336 Oct 25 13:38 encrypt*
-rw-r----- 1 krypton3 krypton3    27 Oct 25 13:38 keyfile.dat
-rw-r----- 1 krypton2 krypton2    13 Oct 25 13:38 krypton3
```
Facem cum spune la finalul enuntului challenge-ului:
```shell
krypton2@krypton:/krypton/krypton2$ mktemp -d
/tmp/tmp.DoPIh6zSKs

krypton2@krypton:/krypton/krypton2$ cd /tmp/tmp.DoPIh6zSKs

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ ln -s /krypton/krypton2/keyfile.dat

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ ls -laF
total 0
drwx------   2 krypton2 krypton2   60 Nov  5 10:35 ./
drwxrwx-wt 103 root     root     2540 Nov  5 10:35 ../
lrwxrwxrwx   1 krypton2 krypton2   29 Nov  5 10:35 keyfile.dat -> /krypton/krypton2/keyfile.dat

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ chmod 777 .
```
Pentru a observa cum se shifteaza alfabetul, aplicam criptarea pe alfabetul plain:
```shell
krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ touch alpha.txt

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ echo "ABCDEFGHIJKLMNOPQRSTUVWXYZ" > alpha.txt

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ /krypton/krypton2/encrypt alpha.txt

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ ls -laF
total 8
drwxrwxrwx   2 krypton2 krypton2  100 Nov  5 10:36 ./
drwxrwx-wt 103 root     root     2540 Nov  5 10:36 ../
-rw-rw-r--   1 krypton2 krypton2   27 Nov  5 10:35 alpha.txt
-rw-rw-r--   1 krypton3 krypton2   26 Nov  5 10:36 ciphertext
lrwxrwxrwx   1 krypton2 krypton2   29 Nov  5 10:35 keyfile.dat -> /krypton/krypton2/keyfile.dat

krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ cat ciphertext
MNOPQRSTUVWXYZABCDEFGHIJKL
```
Acum stim ca A devine M, B devine N, etc.
Cu `tr` facem asocierea inversa (decriptarea):
```shell
krypton2@krypton:/tmp/tmp.DoPIh6zSKs$ echo $(cat /krypton/krypton2/krypton3) | tr 'M-ZA-L' 'A-Z'
CAESARISEASY
```
