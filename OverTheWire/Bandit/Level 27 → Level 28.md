# Level 27 → Level 28

## Level Goal

There is a git repository at `ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo` via the port `2220`. 
The password for the user `bandit27-git` is the same as for the user `bandit27`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. 
This needs git installed locally on your machine.

## Write-Up

Clonam repo-ul local:
```shell
$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
Cloning into 'repo'...
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit27-git@bandit.labs.overthewire.org's password: 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
```
```shell
$ ls -laF      
drwxr-xr-x    - coswin  2 Nov 13:13 repo/
```
Ne ducem in repo si cautam flag-ul:
```shell
$ cd repo

$ ls -laF
drwxr-xr-x  - coswin  2 Nov 13:13 .git/
.rw-r--r-- 68 coswin  2 Nov 13:13 README

$ cat README    
─────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     │ File: README
─────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 │ The password to the next level is: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
─────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```
