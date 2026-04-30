# Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called **-** located in the home directory

## Write-Up

[https://stackoverflow.com/questions/42187323/how-to-open-a-dashed-filename-using-terminal](https://stackoverflow.com/questions/42187323/how-to-open-a-dashed-filename-using-terminal)

```bash
bandit1@bandit:~$ ls -la
total 24
-rw-r-----   1 bandit2 bandit1   33 Oct 14 09:26 -
drwxr-xr-x   2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 150 root    root    4096 Oct 14 09:29 ..
-rw-r--r--   1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root    3851 Oct 14 09:19 .bashrc
-rw-r--r--   1 root    root     807 Mar 31  2024 .profile

bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

Flag: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx