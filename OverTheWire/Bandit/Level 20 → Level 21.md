# Level 20 → Level 21

## Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE**: Try connecting to your own network daemon to see if it works as you think

## Write-Up

Pentru acest challenge ne trebuie 2 instante de shell: una sa deschidem port-ul (sa ii zicem `INSTANCE 1`) si una sa folosim binarul (`INSTANCE 2`)

Pentru a incepe 2 instante folosim comanda `tmux`

Deschidem un port arbitrar (am ales la misto 6767):
```bash
[INSTANCE 1]
bandit20@bandit:~$ nc -lp 6767


```
Intre timp, folosim binarul dat:
```bash
[INSTANCE 2]
bandit20@bandit:~$ ls -la
total 36
drwxr-xr-x   2 root     root      4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root      4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root      3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root     root       807 Mar 31  2024 .profile
-rwsr-x---   1 bandit21 bandit20 15612 Apr  3 15:17 suconnect

bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP.
If it receives the correct password from the other side, the next password is transmitted back.

bandit20@bandit:~$ ./suconnect 6767


```
S-a conectat la port, acum asteapta sa transmitem din partea cealalta (`INSTANCE 1`) parola:
```bash
[INSTANCE 1]
bandit20@bandit:~$ nc -lp 6767
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

```
Daca verificam cealalta instanta, primim un semn bun:
```bash
[INSTANCE 2]
bandit20@bandit:~$ ./suconnect 6767
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
```
Si in `INSTANCE 1` primim direct parola:
```bash
[INSTANCE 1]
bandit20@bandit:~$ nc -lp 6767
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```
Flag: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
