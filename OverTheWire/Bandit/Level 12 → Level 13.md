# Level 12 → Level 13

## Level Goal

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv

## Write-Up

```bash
bandit12@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit13 bandit12 2575 Apr  3 15:17 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
```

Copiez fisierul intr-un directory temporar:

```bash
bandit12@bandit:~$ temp_dir=$(mktemp -d)

bandit12@bandit:~$ cp data.txt $temp_dir

bandit12@bandit:~$ cd $temp_dir

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls -la
total 48
drwx------   2 bandit12 bandit12  4096 Apr  4 19:52 .
drwxrwx-wt 599 root     root     36864 Apr  4 19:52 ..
-rw-r-----   1 bandit12 bandit12  2575 Apr  4 19:52 data.txt
```

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ head data.txt
00000000: 1f8b 0808 00da cf69 0203 6461 7461 322e  .......i..data2.
00000010: 6269 6e00 0136 02c9 fd42 5a68 3931 4159  bin..6...BZh91AY
00000020: 2653 5978 ae89 f600 001c 7fff db7d bfef  &SYx.........}..
00000030: 8ff7 f7ff ffc2 ffcd 7cbd 2ee4 dff9 aff3  ........|.......
00000040: ef7b d577 e9f7 adbd dfbb fbff b001 3b30  .{.w..........;0
00000050: 63a0 6806 8326 400d 0031 0000 00d1 a313  c.h..&@..1......
00000060: 2000 001a 034d 1a19 0000 0032 0681 89a6   ....M.....2....
00000070: 9a32 0da9 934c 6847 9220 0034 0346 9a00  .2...LhG. .4.F..
00000080: d340 3462 0006 d4d3 d41a 064d 0308 6868  .@4b.......M..hh
00000090: 0340 1a19 3264 321b 50f5 00c8 01ea 0d00  .@..2d2.P.......

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ xxd -r data.txt > xyz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file xyz
xyz: gzip compressed data, was "data2.bin", last modified: Fri Apr  3 15:17:20 2026, max compression, from Unix, original size modulo 2^32 566
```

Fisierul este compressed cu gzip, deci ii pun extensia `.gz` si ii dau decompress

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv xyz xyz.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ gzip -d xyz.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file xyz
xyz: bzip2 compressed data, block size = 900k
```

Fisierul este compressed cu bzip2, deci ii pun extensia `.bz2` si ii dau decompress

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv xyz xyz.bz2

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ bzip2 -d xyz.bz2

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file xyz
xyz: gzip compressed data, was "data4.bin", last modified: Fri Apr  3 15:17:20 2026, max compression, from Unix, original size modulo 2^32 20480

```

Din nou gzip

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv xyz xyz.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ gzip -d xyz.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file xyz
xyz: POSIX tar archive (GNU)
```

Fisierul este compressed cu tar, deci ii pun extensia `.tar` si ii dau decompress

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv xyz xyz.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ tar -xf xyz.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file xyz
xyz: cannot open `xyz' (No such file or directory)

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls
data5.bin  data.txt  xyz.tar
```

Si-a dat decompress direct in `data5.bin`

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file data5.bin
data5.bin: POSIX tar archive (GNU)
```

Din nou tar

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv data5.bin data5.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ tar -xf data5.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls
data5.tar  data6.bin  data.txt  xyz.tar
```

Si-a dat decompress in `data6.bin`

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```

Din nou bzip2

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv data6.bin data6.bz2

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ bzip2 -d data6.bz2

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls
data5.tar  data6  data.txt  xyz.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file data6
data6: POSIX tar archive (GNU)
```

Din nou tar

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv data6 data6.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ tar -xf data6.tar

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls
data5.tar  data6.tar  data8.bin  data.txt  xyz.tar.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Fri Apr  3 15:17:20 2026, max compression, from Unix, original size modulo 2^32 49
```

Din nou gzip

```bash
bandit12@bandit:/tmp/tmp.KzqliCWvLa$ mv data8.bin data8.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ gzip -d data8.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ ls
data5.tar  data6.tar  data8  data.txt  xyz.tar.gz

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ file data8
data8: ASCII text

bandit12@bandit:/tmp/tmp.KzqliCWvLa$ cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

Flag: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn