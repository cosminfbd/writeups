# Level 14 → Level 15

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL/TLS encryption.

## Write-Up

In loc de `nc` folosim `ncat` pentru a putea folosi SSL encryption prin flag-ul `--ssl`:

```bash
bandit15@bandit:~$ ncat --help
Ncat 7.94SVN ( https://nmap.org/ncat )
Usage: ncat [options] [hostname] [port]
[...]
      --ssl                  Connect or listen with SSL
[...]
```
```bash
bandit15@bandit:~$ ncat --ssl localhost 30001
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Primim raspunsul:
```bash
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

Flag: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
