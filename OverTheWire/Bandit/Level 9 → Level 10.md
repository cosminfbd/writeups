# Level 9 → Level 10

## Level Goal

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

## Write-Up

```bash
bandit9@bandit:~$ ls -la
total 40
drwxr-xr-x   2 root     root     4096 Oct 14 09:26 .
drwxr-xr-x 150 root     root     4096 Oct 14 09:29 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Oct 14 09:19 .bashrc
-rw-r-----   1 bandit10 bandit9 19382 Oct 14 09:26 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile

bandit9@bandit:~$ strings data.txt | head
Dm|H
d:Bj
pgM,
g%q&N
}}Jae
:AJsC
E!ML
~>#~
+PIqZ
Zf{,
```

Fisierul `data.txt` e plin de garbage, asa ca vom cauta direct caracterele `=`

```bash
bandit9@bandit:~$ strings data.txt | grep "=="
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

Flag: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey