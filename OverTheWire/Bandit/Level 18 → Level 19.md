# Level 18 → Level 19

## Level Goal

The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

## Write-Up
```bash
$ ssh bandit18@bandit.labs.overthewire.org -p 2220
    [...]
Byebye !
Connection to bandit.labs.overthewire.org closed.
```

Intr-adevar, imi da automat logout cand incerc `ssh`

Pot sa intru de pe profilul de la level-ul anterior (`bandit17`) si sa ma uit la ce e in `bandit18`

```bash
$ ssh -i /home/coswin/OverTheWire/level16_17/bandit16key.private bandit17@bandit.labs.overthewire.org -p 2220
[...]

bandit17@bandit:~$ cd ..

bandit17@bandit:/home$ cd bandit18

bandit17@bandit:/home/bandit18$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r-----   1 bandit19 bandit18 3874 Apr  3 15:17 .bashrc
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
-rw-r-----   1 bandit19 bandit18   33 Apr  3 15:17 readme

bandit17@bandit:/home/bandit18$ cat .bashrc
cat: .bashrc: Permission denied

bandit17@bandit:/home/bandit18$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

Evident, n-am nicio permisiune sa il citesc dar e clar ca din cauza lui `.bashrc` ma delogheaza automat

Trebuie sa ma conectez cu ssh la `bandit18` si sa ignor `.bashrc`

...pot sa fac asta daca adaug `bash --norc`:

```bash
$ ssh bandit18@bandit.labs.overthewire.org -p 2220 bash --norc
[...]
bandit18@bandit.labs.overthewire.org's password: [introduc parola]


```
```bash
ls -la
total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r-----   1 bandit19 bandit18 3874 Apr  3 15:17 .bashrc
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
-rw-r-----   1 bandit19 bandit18   33 Apr  3 15:17 readme

cat readme
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

exit


```

Flag: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
