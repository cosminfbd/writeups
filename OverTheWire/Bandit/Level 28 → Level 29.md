# Level 28 → Level 29

## Level Goal
There is a git repository at `ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo` via the port `2220`. 
The password for the user `bandit28-git` is the same as for the user bandit28.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. 
This needs git installed locally on your machine.

## Write-Up
Dupa ce clonam repo-ul, vedem ce avem:
```shell
$ la
Permissions Size User   Date Modified Git Name
drwxr-xr-x     - coswin  2 Nov 13:29   -I .git
.rw-r--r--   111 coswin  2 Nov 13:26   -- README.md

$ cat README.md
─────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     │ File: README.md
─────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 │ # Bandit Notes
   2 │ Some notes for level29 of bandit.
   3 │ 
   4 │ ## credentials
   5 │ 
   6 │ - username: bandit29
   7 │ - password: xxxxxxxxxx
   8 │ 
─────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Nu ne ajuta cu nimic, parola e ascunsa.
Ne uitam in log sa vedem daca gasim ceva:
```shell
$ git log
```
```
commit 801b85fdfda35a72bed5cf6fad21fce92d76dcc9 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Oct 25 13:37:24 2026 +0000

    fix info leak

commit df10da19c2625f7c59e071e16030bd587d8c409d
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Oct 25 13:37:24 2026 +0000

    add missing data

commit 388bcd3bd1bd2a6d07570282372dcc4653fe9649
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:24 2026 +0000

    initial commit of README.md
```
Ultimul commit are mesajul `fix info leak`, deci inainte de asta parola probabil nu era ascunsa. 
Ne uitam la modificarile facute in ultimul commit:
```shell
$ git show HEAD
```
```
commit 801b85fdfda35a72bed5cf6fad21fce92d76dcc9 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Oct 25 13:37:24 2026 +0000

    fix info leak

diff --git a/README.md b/README.md
index 42331d9..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials
 
 - username: bandit29
-- password: Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
+- password: xxxxxxxxxx
```
