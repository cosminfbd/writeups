# Level 26 → Level 27

## Level Goal

Good job getting a shell! Now hurry and grab the password for bandit27!

## Write-Up
```shell
bandit26@bandit:~$ ls -laF
total 44
drwxr-xr-x   3 root     root      4096 Oct 25 13:37 ./
drwxr-xr-x 150 root     root      4096 Oct 25 13:40 ../
-rw-r--r--   1 root     root       220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root      3851 Oct 25 13:21 .bashrc
-rw-r--r--   1 root     root       807 Feb 13  2026 .profile
drwxr-xr-x   2 root     root      4096 Oct 25 13:37 .ssh/
-rwsr-x---   1 bandit27 bandit26 14880 Oct 25 13:37 bandit27-do*
-rw-r-----   1 bandit26 bandit26   258 Oct 25 13:37 text.txt
```
Observam ca `bandit27-do` are setuid.

```shell
bandit26@bandit:~$ ./bandit27-do
Run a command as another user.
  Example: ./bandit27-do id
```
Luam direct parola:
```shell
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
STJLJBRRphMxKB392CT4iOr5CbzPU9ER
```
