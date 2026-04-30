# Level 11 → Level 12

## Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Write-Up

```bash
bandit11@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Oct 14 09:26 .
drwxr-xr-x 150 root     root     4096 Oct 14 09:29 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Oct 14 09:19 .bashrc
-rw-r-----   1 bandit12 bandit11   49 Oct 14 09:26 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile

bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

[image.png]

`tr` nu ma lasa sa fac `a-z ⇒ n-m` pt ca n > m, asa ca facem pe rand `a-m ⇒ n-z` & `n-z ⇒ a-m` + majuscule

```bash
bandit11@bandit:~$ cat data.txt | tr a-mn-z n-za-m | tr A-MN-Z N-ZA-M
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Flag: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
