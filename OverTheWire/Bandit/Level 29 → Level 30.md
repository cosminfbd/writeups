# Level 29 → Level 30

## Level goal

There is a git repository at `ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo` via the port `2220`. 
The password for the user `bandit29-git` is the same as for the user `bandit29`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. 
This needs git installed locally on your machine.

## Write-Up

```shell
coswin@MacBook-Air repo % la
Permissions Size User   Date Modified Git Name
drwxr-xr-x     - coswin  4 Nov 13:05   -I .git
.rw-r--r--   131 coswin  4 Nov 13:05   -- README.md

coswin@MacBook-Air repo % cat README.md 
─────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     │ File: README.md
─────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1 │ # Bandit Notes
   2 │ Some notes for bandit30 of bandit.
   3 │ 
   4 │ ## credentials
   5 │ 
   6 │ - username: bandit30
   7 │ - password: <no passwords in production!>
   8 │ 
─────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Ne uitam in log-uri:
```shell
coswin@MacBook-Air repo % git log
```
```
commit bf3f6e54ee1dd5ea023571ca2abb706d571d66b3 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    fix username

commit 9682addf0b02016cd8f9611a4fd00b53f534ccaa
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    initial commit of README.md
```

Ne uitam in cele 2 commit-uri:
```shell
coswin@MacBook-Air repo % git show HEAD
```
```
commit bf3f6e54ee1dd5ea023571ca2abb706d571d66b3 (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    fix username

diff --git a/README.md b/README.md
index 2da2f39..1af21d3 100644
--- a/README.md
+++ b/README.md
@@ -3,6 +3,6 @@ Some notes for bandit30 of bandit.
 
 ## credentials
 
-- username: bandit29
+- username: bandit30
 - password: <no passwords in production!>
```
```shell
coswin@MacBook-Air repo % git show HEAD~
```
```
commit 9682addf0b02016cd8f9611a4fd00b53f534ccaa
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..2da2f39
--- /dev/null
+++ b/README.md
@@ -0,0 +1,8 @@
+# Bandit Notes
+Some notes for bandit30 of bandit.
+
+## credentials
+
+- username: bandit29
+- password: <no passwords in production!>
+
```

Nimic de ajutor aici.
Poate pe alt branch gasim ceva.
Sa vedem ce branch-uri avem:
```shell
coswin@MacBook-Air repo % git branch
```
```
  dev
* master
```

Ne mutam pe `dev` si ne uitam la commit-uri:
```shell
coswin@MacBook-Air repo % git checkout dev   
Switched to branch 'dev'
Your branch is up to date with 'origin/dev'.

coswin@MacBook-Air repo % git log
```
```
commit 6a3b86581f1c4ba92a2ae86b3d62f95dd20b284f (HEAD -> dev, origin/dev)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    add data needed for development

commit 61589aef97f8764b10513efde8f074277232131c
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    add gif2ascii

commit bf3f6e54ee1dd5ea023571ca2abb706d571d66b3 (origin/master, origin/HEAD, master)
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    fix username

commit 9682addf0b02016cd8f9611a4fd00b53f534ccaa
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    initial commit of README.md
```
Vom gasi flag-ul in cel mai recent commit:
```shell
coswin@MacBook-Air repo % git show HEAD
```
```
commit 6a3b86581f1c4ba92a2ae86b3d62f95dd20b284f (HEAD -> dev, origin/dev)
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Oct 25 13:37:28 2026 +0000

    add data needed for development

diff --git a/README.md b/README.md
index 1af21d3..d395d04 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for bandit30 of bandit.
 ## credentials
 
 - username: bandit30
-- password: <no passwords in production!>
+- password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```
