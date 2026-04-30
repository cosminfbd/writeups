# Level 8 → Level 9

## Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Write-Up

```bash
bandit8@bandit:~$ ls -la
total 56
drwxr-xr-x   2 root    root     4096 Oct 14 09:26 .
drwxr-xr-x 150 root    root     4096 Oct 14 09:29 ..
-rw-r--r--   1 root    root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root     3851 Oct 14 09:19 .bashrc
-rw-r-----   1 bandit9 bandit8 33033 Oct 14 09:26 data.txt
-rw-r--r--   1 root    root      807 Mar 31  2024 .profile

bandit8@bandit:~$ head data.txt
UD0JGdEzC9MvLEFryrg13oTd5Hb07iWd
7GmAoWty7FVrx69vVdHsWI3K7bhXB7ck
XFZ2qtQ5m9FCzyje1e5fCvm2F1TeU5pJ
SigSsDLtaSCPLVAD19uwb7HMhgacgZIQ
n4AyXe6YBg4jxCI962uvCGds9tmRDEC0
X4Jb6zVDJ9UdgbMwRYkNcFY8Ej9DvF1Y
bDl7043OFGqzHtKz5iYpTFi3Zln25Jmw
fhdDKwDN5APtF9E7fQXwnXvotlDBGPxj
hBVAVvsUSGFy4l6G0AXj6Eo3wdbrXo7H
CNGEVMYxOaDE4pwyEo98rmCZKrXm8U4Q
```

Sortam fisierul si verificam liniile unice

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

Flag: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM