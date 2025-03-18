# 🔒 NFS Server Breach: Classified Secret Extraction Write-Up

![image](https://github.com/user-attachments/assets/824e47e7-a30d-48fb-a06a-8e6217835324)
*Caption: The challenge interface showing the NFS breach scenario and instructions.*

![Hacker Banner](https://img.shields.io/badge/Challenge-NFS%20Intrusion-red?style=for-the-badge)  
*Unveiling the stolen secret from a packet capture with style and precision!*

---

## 📜 Challenge Overview

An intruder breached our network, targeting an NFS server hosting backup files, and stole a classified secret. The only clue? A packet capture file (`challenge.pcapng`) located in `~/Desktop` on a Kali Linux VM. Our mission: analyze the PCAP and uncover the stolen data. Let’s dive in! 🕵️‍♂️

---

## 🛠️ Step 1: Initial Setup and Packet Capture Analysis

I kicked things off by spawning the VM and verifying the file:

```bash
ubuntu@tryhackme:~/Desktop$ ls -l
total 72
-rw-rw-r-- 1 ubuntu ubuntu 66604 Mar  6 16:39 challenge.pcapng
-rwxrwxr-x 1 ubuntu ubuntu   166 Feb 27  2022 mate-terminal.desktop
```
With challenge.pcapng confirmed, I launched Wireshark:
```bash
wireshark challenge.pcapng &
```
Filtered for NFS traffic since the target was an NFS server:
![image](https://github.com/user-attachments/assets/dfd893c5-2556-45d2-9cb7-0a1bd0ba251e)

Spotted multiple READ_PLUS operations—NFSv4.1’s advanced read function—hinting at data extraction.

## 🔍 Step 2: Analyzing the First READ_PLUS Packet

The first key packet (source port 2049, NFS default) delivered 61 bytes of readable data:

```bash
0000   00 0c 29 76 32 b1 00 50 56 e8 af 99 08 00 45 00   ..)v2..PV.....E.
0010   00 e0 03 7f 00 00 80 06 59 61 0a 0a 77 9d ac 10   ........Ya..w...
0020   af 80 08 01 03 42 47 12 97 2d 35 98 3b fc 50 18   .....BG..-5.;.P.
0030   fa f0 0e 7b 00 00 80 00 00 b4 ac a9 d8 06 00 00   ...{............
...
00b0   00 39 41 72 63 68 69 76 65 20 50 61 73 73 77 6f   .9Archive Passwo
00c0   72 64 0a 0a 39 30 65 62 37 37 32 33 61 36 35 37   rd..90eb7723a657
00d0   62 36 35 39 37 31 30 30 61 61 66 65 66 31 37 31   b6597100aafef171
00e0   64 39 66 32 20 28 6d 64 35 29 0a 00 00 00         d9f2 (md5)....
```

Extracted and converted the payload:

```bash
echo "39417263686976652050617373776f72640a0a39306562373732336136357b3635393731303061616665663137316439663220286d6435290a" | xxd -r -p
```
### Output:
```bash
9Archive Password

90eb7723a657b6597100aafef171d9f2 (md5)
```

* File Handle: 87 7b c9 67 61 33 e6 ed
* Data Length: 61 bytes
* Content: A header and an MD5 hash—possibly a password clue? 🤔

## 📦 Step 3: Analyzing the Second READ_PLUS Packet
Another READ_PLUS packet with the same file handle dropped a bigger payload:
```bash
0000   00 0c 29 76 32 b1 00 50 56 e8 af 99 08 00 45 00   ..)v2..PV.....E.
0010   03 cc 03 a7 00 00 80 06 56 4d 0a 0a 77 9d ac 10   ........VM..w...
0020   af 80 08 01 03 42 47 12 a8 c5 35 98 4f a0 50 18   .....BG...5.O.P.
0030   fa f0 5f 58 00 00 80 00 03 a0 c0 a9 d8 06 00 00   .._X............
...
00b0   03 26 50 4b 03 04 14 00 09 00 08 00 d4 02 67 5a   .&PK..........gZ
00c0   84 5a 68 e1 6a 02 00 00 66 03 00 00 0b 00 1c 00   .Zh.j...f.......
00d0   73 65 63 72 65 74 73 2e 70 6e 67 55 54 09 00 03   secrets.pngUT...
...
03d0   bf 02 00 00 00 00 00 00
```

* **File Handle:** 87 7b c9 67 61 33 e6 ed
* **Payload:** A ZIP archive with secrets.png!

Saved the ZIP:
```bash
xxd -r -p <<EOF > stolen.zip
0326504b0304140009000800d402675a845a68e16a020000660300000b001c00736563726574732e706e675554090003d0cbc967f9cbc96775780b000104f50100000414000000c01c27f8cfe35dd73be6a8aeb8ea2d920dbeab8d5e0b55d090da1ade3897419e92588225c379cf5ee288bb32321b0222a8efabbb8832f701466452b81798deb8298154809eedd4301aa88022318156cc6889148bd104e06fd81ea290d02e11d3d0c7e2318e0172524edeb7cc98f407993f66b5463bcc95e6618b12333dc5de558d4d59ea31f2c1445ed4c939630dfe3c6d241d4cf4f5b1f30e646875d8591aa9c5cfbb2cf0a4d7b6638a0946e39b0a1da2a4869a210b5d46fce1ddae4415d6327d2e9776185bf827d2d01efda78349677e69e0bde769eefeb2a9c83c680b8ad75d061d5fe50690a6a77ff3dc17a5e97d686d8157f36559a84525341e25d992ec57003d587c496ecead50e14d48098c899ccbff3721698f5d2214cb4b104da5728e370767f0568d34a0bb3841052932cd3b7332ea59cb7d431bba2f75a33cc3ae69b7809200b06a6b2159a4c71db4dfe9bec9fbf52442b68b8e1d8b97800d058d7a121445ff5a142fd85c22e89dde607189c1dc24d742fd781c65abd7941af4b1e89bf623d70c970df7a446b562256ea37a7cca3538fcc4114da7f2f82818f6cc7826a076843134d089272dc66051c0fc4e95e5041299d805c5e0853db6898e04bfd4e2c064a7f667f9ebbc21b746d45edd830f9e40cfa72d0dd017f03f41f2cc3910f36cd6a3908a3700f199e70ec47104aacdfae61f378b003813f37d0f0324898f36a4865a6fcd6e6a08b0681cc141be2123f9912d50d80272e624358ec842d9d12883b7d4b9a842e08da63aa9fd595026f536d76105f5e0fd89cfce058f2720e4afe5a01b1710423c3b8246d5b58e42dcf6fff41673c231644c45136076df534663ae69e028f2e7ba504b0708845a68e16a02000066030000504b01021e03140009000800d402675a845a68e16a020000660300000b0018000000000000000000a48100000000736563726574732e706e675554050003d0cbc96775780b000104f50100000414000000504b0506000000000100010051000000bf0200000000
EOF
```

Verified:
```bash
ubuntu@tryhackme:~$ ls
Desktop    Downloads  Pictures  Templates  snap
Documents  Music      Public    Videos     stolen.zip
```
```bash
stolen.zip: Zip archive data, at least v2.0 to extract, encrypted
```

## 🔐 Step 4: Decoding the Password
The ZIP was encrypted. I tested the hash as the password:
```bash
unzip -P 90eb7723a657b6597100aafef171d9f2 stolen.zip
```

No dice. The (md5) tag meant it was the hash of the password. I used an online MD5 decoder and input <mark>90eb7723a657b6597100aafef171d9f2</mark> . It cracked it: the password was **<mark>avengers</mark>**. 🦸‍♂️

## 🖼️ Step 5: Extracting secrets.png
Unlocked the ZIP:
```bash
unzip -P avengers stolen.zip
```
Output:
```bash
Archive: stolen.zip
  inflating: secrets.png
```
Output: secrets.png: PNG image data

## 🎉 Step 6: Uncovering the Flag
Opening secrets.png revealed a QR code. Scanned it with my mobile phone:
![image](https://github.com/user-attachments/assets/107d9205-adb8-4b34-a1ae-159e1ce791e2)

Output:
```bash
THM{n0t_s3cur3_f1l3_sh4r1ng}
```
The flag: **<mark>THM{n0t_s3cur3_f1l3_sh4r1ng}!</mark>** Victory! 🎯

## 🌟 Conclusion
The intruder stole an encrypted ZIP (<mark>stolen.zip</mark>) containing <mark>secrets.png</mark> via NFS. The first <mark>READ_PLUS</mark> packet gave us the MD5 hash of the password (<mark>avengers</mark>), cracked online. The second packet delivered the ZIP, and <mark>secrets.png hid</mark> a QR code with the flag: <mark>THM{n0t_s3cur3_f1l3_sh4r1ng}</mark>. A lesson in the dangers of insecure file sharing! 🚨

# <mark>Final Flag: THM{n0t_s3cur3_f1l3_sh4r1ng}</mark>

*Powered by TryHackMe's AttackBox, Wireshark, and a bit of superhero flair!*
