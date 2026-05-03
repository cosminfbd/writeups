# Level 16 → Level 17

## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Write-Up

Scanam port-urile de la 31000 la 32000:
```bash
bandit16@bandit:~$ nmap -p 31000-32000 localhost
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-05-03 15:49 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

```

Le luam la rand sa vedem care are SSL:
```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31046
CONNECTED(00000003)
4067F0F7FF7F0000:error:0A0000F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:398:
---
no peer certificate available
---
No client certificate CA names sent
---
SSL handshake has read 293 bytes and written 300 bytes
Verification: OK
---
New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 0 (ok)
---
```

⬆️ Nu are SSL. Il incercam pe urmatorul (31518):
```
bandit16@bandit:~$ openssl s_client -connect localhost:31518
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 6F10BC2C366B57310C958946DC84B13CB3C04038A0E415315B96756420BF9667
    Session-ID-ctx: 
    Resumption PSK: E068C482F7F90A08328B58A1251C47F132880EFF86D91B91F47C43BBB2DAFA711A6EEF32252CA6311D51BA7B38BEF0A4
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - ae 6a c0 90 3d eb f9 5f-2c e5 e2 42 a7 83 98 c8   .j..=.._,..B....
    0010 - 4f e9 e5 22 fa 85 61 d3-d0 13 33 c2 18 9b 9c cf   O.."..a...3.....
    0020 - 04 d8 ef c9 75 99 ee 01-13 2d 14 90 46 78 1b 85   ....u....-..Fx..
    0030 - 26 5b a9 37 0d b1 9c 9c-a8 22 15 58 b3 98 d3 3a   &[.7.....".X...:
    0040 - f4 3b aa f6 d6 a2 bf 99-fb 3a 7a 0a be b0 ad df   .;.......:z.....
    0050 - 73 af b0 2d 1f 33 98 1c-e1 42 9d 04 7e 75 47 50   s..-.3...B..~uGP
    0060 - 3b 4e 14 04 68 87 58 db-47 23 fc 8d 3d aa e5 61   ;N..h.X.G#..=..a
    0070 - fb d6 2e b4 99 94 c5 79-98 64 9a dc 42 ba a6 46   .......y.d..B..F
    0080 - f8 3f 0c ec ca 74 7f d8-07 5b 40 5a 5f 3e 20 04   .?...t...[@Z_> .
    0090 - 5d 8c bd b2 a8 29 1c 85-f2 87 4f 81 2a 6a 78 31   ]....)....O.*jx1
    00a0 - fa 00 f6 aa fa 5a 13 8e-41 b3 48 34 74 02 39 12   .....Z..A.H4t.9.
    00b0 - e8 eb 0d 3f db e7 3b 42-b3 ae 82 fd c8 60 94 1a   ...?..;B.....`..
    00c0 - 0b 3c 47 ff c4 88 90 1e-9a 90 4e 30 24 5b 83 b9   .<G.......N0$[..
    00d0 - b4 cf de 36 82 0b e8 67-84 11 a2 ee 19 eb 8f f7   ...6...g........

    Start Time: 1777823817
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: E456CB78348B3BEB3609852331D88C438D2245B0766D7FCC220272311566B2B1
    Session-ID-ctx: 
    Resumption PSK: 0288A34673001B2AB16B4F9B4C88E57227634C89B39BFF7C589D5C260E57057F8A4A950F65D018BBDA34C1F7FCFE0A7C
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - ae 6a c0 90 3d eb f9 5f-2c e5 e2 42 a7 83 98 c8   .j..=.._,..B....
    0010 - 8d c4 25 e6 70 d6 e7 6e-68 29 1a 20 74 d5 54 7b   ..%.p..nh). t.T{
    0020 - 3d f8 3c c1 7a 8b 45 f7-c5 08 7d 19 53 eb 8e 22   =.<.z.E...}.S.."
    0030 - 8b 7d 10 b2 7e 91 53 5e-17 86 00 83 72 d1 70 55   .}..~.S^....r.pU
    0040 - c0 f1 47 5a c1 bf 64 00-8a 7e ae 5f 08 1a bf 2c   ..GZ..d..~._...,
    0050 - 35 db 28 cb 31 0e 58 61-49 ac 18 73 19 c2 f3 e1   5.(.1.XaI..s....
    0060 - 71 b9 0c 4f 6c 7a 77 6c-0a b5 d8 01 a8 d9 1c a6   q..Olzwl........
    0070 - e3 14 8e 58 83 3c fa 1a-9d 61 54 c9 06 02 e4 c1   ...X.<...aT.....
    0080 - 6e af 32 83 1c 03 81 63-24 46 9a 2e 01 90 80 43   n.2....c$F.....C
    0090 - 71 21 9c 2c 3e 3c 6f 07-97 0a 41 9a 7d a3 c4 c0   q!.,><o...A.}...
    00a0 - 31 c4 ce 90 28 d2 e0 cf-e1 4e 52 80 1d 48 fb f7   1...(....NR..H..
    00b0 - 1e 4f 9c 75 f9 26 e7 bd-f4 26 65 03 69 ba c6 79   .O.u.&...&e.i..y
    00c0 - 7a 06 e7 09 85 a4 c6 27-0a c6 d5 e8 0a a9 6d f8   z......'......m.
    00d0 - 7a 28 90 0d a4 36 13 4f-29 98 73 9e 64 87 37 98   z(...6.O).s.d.7.

    Start Time: 1777823817
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
^C
```

Perfect, are SSL. Ne conectam la el si ii trimitem flag-ul:
```bash
bandit16@bandit:~$ ncat --ssl localhost 31518
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
^C
```

Din pacate este unul din port-urile pacalitoare, care intoarce ce ii trimitem. Trecem la urmatorul port (31691).
```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31691
CONNECTED(00000003)
4067F0F7FF7F0000:error:0A0000F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:398:
---
no peer certificate available
---
No client certificate CA names sent
---
SSL handshake has read 293 bytes and written 300 bytes
Verification: OK
---
New, (NONE), Cipher is (NONE)
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 0 (ok)
---
```

⬆️ Nu are SSL. Trecem la 31790.

```
bandit16@bandit:~$ openssl s_client -connect localhost:31790
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: C574531117108B50C6B99D2E47262555C8701D81D2F8E23E797E856DC1A24BD7
    Session-ID-ctx: 
    Resumption PSK: 6B108DCEE0D336CDED854145BB751FBEE8666216EAAF292E6FD14B6307C407D887B1AA21557B0666AD8BE4A9798A275A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - c5 d5 ea 18 2a c8 56 2f-90 b8 a7 52 10 1d 24 7d   ....*.V/...R..$}
    0010 - ca 3d 9d 87 db bd f6 63-5a 5a 84 05 62 a6 69 a2   .=.....cZZ..b.i.
    0020 - 55 6f e8 39 e1 74 0d c3-65 b8 c3 45 f0 ef 04 5a   Uo.9.t..e..E...Z
    0030 - 5b 29 09 20 ca 45 83 d0-8f 7f b6 b6 a7 2b 1a 1a   [). .E.......+..
    0040 - 3a d0 54 51 88 05 d6 6f-04 31 be fa 4a 82 e2 62   :.TQ...o.1..J..b
    0050 - 34 c6 d4 55 63 60 44 b6-32 49 f7 82 3f 7e a1 0d   4..Uc`D.2I..?~..
    0060 - a6 0f 8b 15 1a 26 40 29-95 64 5c 32 53 5b 09 bb   .....&@).d\2S[..
    0070 - 10 09 e5 43 3c 6d 76 30-70 dd dd b3 d8 db eb b0   ...C<mv0p.......
    0080 - e9 f6 9f 18 00 98 1c 99-0f be 99 6b dd 06 68 4e   ...........k..hN
    0090 - 4e 47 2f 0b ac 8b 5e 73-20 3f 78 c6 2a ef 78 9c   NG/...^s ?x.*.x.
    00a0 - 7b 8c 11 68 bd 81 46 e8-05 0f 72 b3 bb c3 f7 2d   {..h..F...r....-
    00b0 - 03 11 a2 0b 3b 77 e8 f1-02 36 8d be e0 ca b9 38   ....;w...6.....8
    00c0 - cf b0 ef 10 62 00 8e 27-25 6b 93 fa cd 9e 17 51   ....b..'%k.....Q
    00d0 - d7 68 40 68 3a c0 5b c6-b1 cd cf 37 a1 93 9b e8   .h@h:.[....7....

    Start Time: 1777824207
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: CC3513066C04C9CA77AB5AB4C62870AAAB4D47C61B5123DF21FB0F0472A17C0F
    Session-ID-ctx: 
    Resumption PSK: 9621892FA0BDB588E666C6C1D70ADB2D9E0396FB618C923CD4F24F6DDE5356FCA86D402133137E174BFF982F16F75997
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - c5 d5 ea 18 2a c8 56 2f-90 b8 a7 52 10 1d 24 7d   ....*.V/...R..$}
    0010 - ea fd f6 d6 96 5e 60 97-b8 ee d8 90 d1 73 c2 a6   .....^`......s..
    0020 - bd f6 b7 82 b6 2f d6 15-f5 f7 b1 e9 e8 5a 2c e3   ...../.......Z,.
    0030 - 34 fa 85 20 c3 58 80 a2-54 68 03 f7 14 80 db 7d   4.. .X..Th.....}
    0040 - 9a 1b 89 36 6c 25 30 4b-42 a7 96 b0 bc ef 43 df   ...6l%0KB.....C.
    0050 - 20 3c fc 7c 8e 87 e1 bf-1d 25 eb a3 4a 63 e7 a9    <.|.....%..Jc..
    0060 - af 64 a3 be 9b be 6f 51-fb 0b 5c 0b 88 ed 7b 03   .d....oQ..\...{.
    0070 - 9e 54 88 57 1b 0b 5d bc-ea d0 25 12 17 d9 aa 2e   .T.W..]...%.....
    0080 - f7 ff 49 1f 08 64 6e a4-6b df 51 95 42 9f d1 6d   ..I..dn.k.Q.B..m
    0090 - a8 c8 ca 63 a4 be f7 e8-a5 a9 0e 30 e5 78 3c 21   ...c.......0.x<!
    00a0 - ad 9a cf 71 df 78 1c 26-a2 79 3a cb 11 83 ef b9   ...q.x.&.y:.....
    00b0 - 58 f8 82 75 82 d0 c9 6c-8c 26 17 88 ab 0e f9 a3   X..u...l.&......
    00c0 - 61 e7 89 0c 08 28 0a 25-69 92 c7 b6 76 2e f9 1c   a....(.%i...v...
    00d0 - fe a7 c3 ea 4d 20 60 cb-ec 42 5f ac c0 a6 9f 2a   ....M `..B_....*

    Start Time: 1777824207
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
^C
```

⬆️ Acesta are SSL si ne conectam la el:
```bash
bandit16@bandit:~$ ncat --ssl localhost 31790
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
Primim raspunsul:
```
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

^C
```

Iesim de pe server si salvam cheia RSA:
```bash
bandit16@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```
(LOCAL):
```bash
~$ cd /home/coswin/OverTheWire/

~/OverTheWire/$ mkdir level16_17

~/OverTheWire/$ cd /home/coswin/OverTheWire/level16_17/

~/OverTheWire/level16_17$ echo "-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
" > bandit16key.private
```
Securizam cheia:
```bash
~/OverTheWire/level16_17$ chmod 400 bandit16key.private
```
Ne conectam la urmatorul nivel astfel:
```bash
$ ssh -i /home/coswin/OverTheWire/level16_17/bandit16key.private bandit17@bandit.labs.overthewire.org -p 2220
```
