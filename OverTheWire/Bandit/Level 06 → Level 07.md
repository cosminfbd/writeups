# Level 6 → Level 7

## Level Goal

The password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

## Write-Up

```bash
bandit6@bandit:~$ ls -la
total 20
drwxr-xr-x   2 root root 4096 Oct 14 09:25 .
drwxr-xr-x 150 root root 4096 Oct 14 09:29 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Oct 14 09:19 .bashrc
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
```

Nimic useful in ~ si spune **somewhere on the server**, deci cautam in tot server-ul.

```bash
bandit6@bandit:~$ cd ..

bandit6@bandit:/home$ cd ..

bandit6@bandit:/$ find -user bandit7 -group bandit6 -size 33c
find: ‘./proc/tty/driver’: Permission denied
find: ‘./proc/1/task/1/fd’: Permission denied
find: ‘./proc/1/task/1/fdinfo’: Permission denied
find: ‘./proc/1/task/1/ns’: Permission denied
find: ‘./proc/1/fd’: Permission denied
[...]
./var/lib/dpkg/info/bandit7.password
find: ‘./var/lib/amazon’: Permission denied
find: ‘./var/crash’: Permission denied
find: ‘./var/cache/apt/archives/partial’: Permission denied
find: ‘./var/cache/pollinate’: Permission denied
find: ‘./var/cache/private’: Permission denied
[...]
find: ‘./etc/ssl/private’: Permission denied
find: ‘./root’: Permission denied
find: ‘./manpage/manpage3-pw’: Permission denied
find: ‘./dev/mqueue’: Permission denied
find: ‘./dev/shm’: Permission denied
```

`./var/lib/dpkg/info/bandit7.password` e singurul fisier in care avem permisiuni

```bash
bandit6@bandit:/$ file ./var/lib/dpkg/info/bandit7.password
./var/lib/dpkg/info/bandit7.password: ASCII text

bandit6@bandit:/$ cat ./var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

Flag: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
