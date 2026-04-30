# Level 2 → Level 3

## Level Goal

The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory

## Write-Up

[https://stackoverflow.com/questions/23019471/how-can-i-go-to-a-directory-whose-file-name-has-spaces-between-them-in-the-linux](https://stackoverflow.com/questions/23019471/how-can-i-go-to-a-directory-whose-file-name-has-spaces-between-them-in-the-linux)

```bash
bandit2@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 150 root    root    4096 Oct 14 09:29 ..
-rw-r--r--   1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root    3851 Oct 14 09:19 .bashrc
-rw-r--r--   1 root    root     807 Mar 31  2024 .profile
-rw-r-----   1 bandit3 bandit2   33 Oct 14 09:26 --spaces in this filename--

bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename--
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

Flag:  MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx