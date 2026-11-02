# Level 25 → Level 26

## Level Goal

Logging in to bandit26 from bandit25 should be fairly easy… 
The shell for user bandit26 is not /bin/bash, but something else. 
Find out what it is, how it works and how to break out of it.

>NOTE: if you’re a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.


## Write-Up

Vom cauta in `/etc/passwd` ce shell foloseste `bandit26`:
```shell
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
Deci executa `/usr/bin/showtext` ca shell. Sa vedem ce face:
```shell
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
Deci deschide cu `more` fisierul `text.txt`.
Also, avem si o cheie de ssh:
```shell
bandit25@bandit:~$ ls
bandit26.sshkey
```
Ne vom conecta cu cheia la urmatorul nivel:
```shell
$ ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!

[...]
  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to bandit.labs.overthewire.org closed.
```
Banner-ul acela este prea mic pentru `more` ca sa faca ceva, asa ca ne scoate. 
Ne vom conecta cu fereastra terminalului micsorata la maxim.
Fiind in `more`, putem apasa `v` pentru a intra in `vim`.
Acolo, putem mari fereastra inapoi la normal.
Din `vim` putem modifica shell-ul in bash cu `:set shell=/bin/bash`, apoi executam bash-ul cu `:shell`.
Acum suntem conectati la `bandit26` cu bash:
```shell
bandit26@bandit:~$ 
```
