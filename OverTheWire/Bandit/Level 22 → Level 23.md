# Level 22 → Level 23

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE**: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Write-Up

Ne uitam in `/etc/cron.d/`, cum sugereaza cerinta
```bash
bandit22@bandit:~$ cd /etc/cron.d/

bandit22@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job  sysstat
```

E destul de clar ca trebuie sa ne uitam in `ronjob_bandit23` (bandit23 = urmatorul nivel)
```bash
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
Gasim un shell script. Sa ne uitam in el:
```bash
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
Din script intelegem ca salveaza username-ul in variabila `myname` si genereaza un hash MD5 pe baza textului `I am user $myname`.
Apoi salveaza parola user-ului curent in `/tmp/$mytarget`.

Spre exemplu: pentru `bandit23` (ce ne trebuie noua), genereaza hash pe baza `I am user bandit23`

Daca il rulam nu ne ajuta, fiindca `myname` va primi valoarea `bandit22` si noua ne trebuie `bandit23`

Atunci hai sa generam singuri hash-ul pe baza username-ului `bandit23`:
```bash
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```
⬆️ Acesta este hash-ul, acum trebuie sa luam parola din `/tmp`:
```bash
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
Flag: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
