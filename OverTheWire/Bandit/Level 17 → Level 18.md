# Level 17 → Level 18

## Level Goal

There are 2 files in the homedirectory: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old** and **passwords.new**

## Write-Up

```bash
bandit17@bandit:~$ ls -la
total 36
drwxr-xr-x   3 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r-----   1 bandit17 bandit17   33 Apr  3 15:17 .bandit16.password
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit18 bandit17 3300 Apr  3 15:17 passwords.new
-rw-r-----   1 bandit18 bandit17 3300 Apr  3 15:17 passwords.old
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .ssh
```

Folosim `diff` in modul context (`-c`):
```bash
bandit17@bandit:~$ diff -c passwords.old passwords.new
*** passwords.old       2026-04-03 15:17:42.564183522 +0000
--- passwords.new       2026-04-03 15:17:42.568157729 +0000
***************
*** 39,45 ****
  GbeMalDIl63fw0N8bqzfCX87m7MHDDUK
  HsCNp4XQst75r0n1xolac4J7Dd8QihaB
  aFoOOJevxDDrih3wldX1AFtnB9xAiHBp
! 390zFj2NETFVZkqYw8UEFdN6h40oGVtT
  tZtZOCHaAOVbz1xgH0bNXydD9iMHMUk8
  q2SDmQDVYZKDmqTS0nmz6SfNbAbxUpYq
  cVGft1jxyTruNSPCLpOnHV4maGb5UgDd
--- 39,45 ----
  GbeMalDIl63fw0N8bqzfCX87m7MHDDUK
  HsCNp4XQst75r0n1xolac4J7Dd8QihaB
  aFoOOJevxDDrih3wldX1AFtnB9xAiHBp
! x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
  tZtZOCHaAOVbz1xgH0bNXydD9iMHMUk8
  q2SDmQDVYZKDmqTS0nmz6SfNbAbxUpYq
  cVGft1jxyTruNSPCLpOnHV4maGb5UgDd
```

Flag: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
