# Level 14 → Level 15

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Write-Up

(Citeste **Bandit Level 13 → Level 14** pentru conectare)

Acum, pentru ca suntem **bandit14**, avem acces la parola din **/etc/bandit_pass/bandit14** mentionata in challenge-ul precedent.

```bash
bandit14@bandit:~$ cd /etc/bandit_pass/

bandit14@bandit:/etc/bandit_pass$ cat bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

Acum ne conectam la **localhost** cu netcat si introducem flag-ul.

```bash
bandit14@bandit:/etc/bandit_pass$ nc localhost 30000
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

Raspunsul primit este:

```bash
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Flag: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo