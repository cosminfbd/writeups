# Level 21 → Level 22

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Write-Up

```bash
bandit21@bandit:~$ cd /etc/cron.d/

bandit21@bandit:/etc/cron.d$ ls -la
total 60
drwxr-xr-x   2 root root  4096 Apr  3 15:20 .
drwxr-xr-x 128 root root 12288 Apr  3 15:20 ..
-r--r-----   1 root root    47 Apr  3 15:18 behemoth4_cleanup
-rw-r--r--   1 root root   123 Apr  3 15:10 clean_tmp
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit22
-rw-r--r--   1 root root   122 Apr  3 15:17 cronjob_bandit23
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-r--r-----   1 root root    48 Apr  3 15:19 leviathan5_cleanup
-rw-------   1 root root   138 Apr  3 15:19 manpage3_resetpw_job
-rwx------   1 root root    52 Apr  3 15:20 otw-tmp-dir
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat

```

Cel mai intuitiv ar fi sa ne uitam in `cronjob_bandit22`
```bash
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
Trebuie sa ne uitam in `/usr/bin/cronjob_bandit22.sh`
```bash
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
E un shell script care pune parola in `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`
```bash
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```
FLag: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
