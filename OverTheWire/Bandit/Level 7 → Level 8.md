# Level 7 → Level 8

## Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Write-Up

```bash
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x   2 root    root       4096 Oct 14 09:26 .
drwxr-xr-x 150 root    root       4096 Oct 14 09:29 ..
-rw-r--r--   1 root    root        220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root       3851 Oct 14 09:19 .bashrc
-rw-r-----   1 bandit8 bandit7 4184396 Oct 14 09:26 data.txt
-rw-r--r--   1 root    root        807 Mar 31  2024 .profile

bandit7@bandit:~$ head data.txt
peroration's	a9aUjV0EDU4p4oiy1MECWUbZx67GqDIN
benefactress	J5Qj0V9NvcXtjf5i9pWCDcWwqLpXrF3j
Lubbock	GjfK8Mo1FyG2NZs0KdBMaJlCLgTIAJA9
dispossession's	dIOOFe0Cfv2NkSTwQl43yRAerDOWTvpH
libidos	vTCZdLjTG02C1vbuJFxG2vqpvmIllv8Z
flailed	3uZIT1mgZe2G4HjnxlL8xQ9dx2sUsmVc
cyclone's	cpqxy7fYUJY5Ng5couwcih5GU285irTN
curt	dz9MYBvtkGaAsQmOs5r964zm0c3OAvQY
amphitheater's	RG06ahKLryAUEdZbFAIqDU2DvrKq9lYV
infrequent	prgVPbuC3H3BHxzhsybUplbyVRdljiKI
```

Fisierul `data.txt` contine un numar urias de perechi key-value si trebuie sa gasim unde se afla key-ul “millionth”

```bash
bandit7@bandit:~$ grep "millionth" data.txt
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

Flag: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc