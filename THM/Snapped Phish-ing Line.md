# Pictures and some sentence
![image](https://github.com/user-attachments/assets/0fdf665a-3cba-4435-b0b8-eb46575e6a25)
Apply learned skills to probe malicious emails and URLs, exposing a vast phishing campaign.

 Disclaimer

Based on real-world occurrences and past analysis, this scenario presents a narrative with invented names, characters, and events.

Please note: The phishing kit used in this scenario was retrieved from a real-world phishing campaign. Hence, it is advised that interaction with the phishing artefacts be done only inside the attached VM, as it is an isolated environment. 

An Ordinary Midsummer Day...

As an IT department personnel of SwiftSpend Financial, one of your responsibilities is to support your fellow employees with their technical concerns. While everything seemed ordinary and mundane, this gradually changed when several employees from various departments started reporting an unusual email they had received. Unfortunately, some had already submitted their credentials and could no longer log in.

You now proceeded to investigate what is going on by:

    Analysing the email samples provided by your colleagues.
    Analysing the phishing URL(s) by browsing it using Firefox.
    Retrieving the phishing kit used by the adversary.
    Using CTI-related tooling to gather more information about the adversary.
    Analysing the phishing kit to gather more information about the adversary.

### Who is the individual who received an email attachment containing a PDF?

Find the user who has a .pdf from the attachment. There are 5 users.

![image](https://github.com/user-attachments/assets/dff5d747-15d3-4add-b5bc-3123e9471d22)

![image](https://github.com/user-attachments/assets/b3439d2c-85eb-4350-9fc6-6ee622ac2bb2)

![image](https://github.com/user-attachments/assets/fe56ef57-c4c4-4938-8a4d-492806b63617)

![image](https://github.com/user-attachments/assets/529ba642-0709-44a4-a488-cda67e6e9594)

![image](https://github.com/user-attachments/assets/9314b0f7-a5ea-42ff-8c34-c0bf151080ed)
```
William McClean
```

### What email address was used by the adversary to send the phishing emails?
![image](https://github.com/user-attachments/assets/69d54e76-cc57-422f-87f9-f09badf939ad)
<br> check the headers
```
Accounts.Payable@groupmarketingonline.icu
```
### What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)
<br>save the .html file and open itin a text editor
![image](https://github.com/user-attachments/assets/1f39adcb-3465-45cd-b452-ddabb6196fb1)

![image](https://github.com/user-attachments/assets/4044254a-2908-437a-9d8c-568a7980be13)

copy that link then go to cyberchef to defang it. Note: Defanging makes the URL link unclickable.

![image](https://github.com/user-attachments/assets/d38fb117-8e5a-4cbe-8ca4-a93718db05d9)

```
hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error
```
### What is the URL to the .zip archive of the phishing kit? (defanged format)
<br> as you can see from the last question answer there is a domain "kennaroads.buzz/data" might be useful to 
browse the .zip

![image](https://github.com/user-attachments/assets/e6a78968-df25-49dd-ba71-1982fc77f46d)

copy that directory then defang it

![image](https://github.com/user-attachments/assets/1de4e87c-15bf-4e67-b217-9b15fd793321)

```
hxxp[://]kennaroads[.]buzz/data/Update365[.]zip
```

### What is the SHA256 hash of the phishing kit archive?
![image](https://github.com/user-attachments/assets/5601f022-ad45-4ce2-9381-53fb85361bac)
```
ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686
```


### When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)
<br> After getting the SHA256 has of the archive file, we can check the date from virustotal using the 
SHA256.
![image](https://github.com/user-attachments/assets/8813430c-aad2-4f13-8083-6299b53026e5)
```
2020-04-08 21:55:50 UTC
```
### When was the SSL certificate the phishing domain used to host the phishing kit archive first logged? (format: YYYY-MM-DD)
<br> from the virustotal navigate to the relations tab to see the SSL certificate domain kennaroads.buzz
![image](https://github.com/user-attachments/assets/a54f3b65-8118-4643-801a-5a8e2626073d)
```
2020-06-25
```

### What was the email address of the user who submitted their password twice?
<br> let's go back from the kennaroads.buzz/data/ we can see there is a folder Update365
![image](https://github.com/user-attachments/assets/a7686350-1beb-49cc-8977-0480aa39dac6)
<br> there is a log.txt that might has records.

![image](https://github.com/user-attachments/assets/79414050-88d6-42df-a07a-b96f12c2433a)
Here is the contents of log.txt we manually find ctrl + f to find "Password" and highlight all
![image](https://github.com/user-attachments/assets/60fa4a2f-6fba-4f3a-a6ea-00addd31d831)
We found that user has submitted the passwird twince.
```
michael.ascot@swiftspend.finance
```

### What was the email address used by the adversary to collect compromised credentials?
<br> I found each of the .php file which contains email address and I found a suspicous one
from submit.php
![image](https://github.com/user-attachments/assets/6ca3fac0-121e-4f8b-80a4-f787edf06f69)
```
m3npat@yandex.com
```

### The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?
<br> from the terminal go to /Update365/office365 and type the command grep -r @email.com . which the -r is recursive.
![image](https://github.com/user-attachments/assets/6040ff47-3805-4af9-a9f5-88dbe1ccef4d)
```
jamestanner229@gmail.com
```
### What is the hidden flag?
<br> I tried using 'find . -type f -name "*.txt" to navigate flag.txt which theres no output
![image](https://github.com/user-attachments/assets/0844d981-7303-4a15-b003-78f9f823460b)
I also tried decoding the url which only outputs dCode which there are no clues

     http://kennaroads.buzz/data/Update365/office365/c845d67f0d018a529437d9611f4e9803/53D0bG17435280684682deae52fa0a44c81fa287adaa06e94682deae52fa0a44c81fa287adaa06e94682deae52fa0a44c81fa287adaa06e94682deae52fa0a44c81fa287adaa06e94682deae52fa0a44c81fa287adaa06e9

Finally, I manually brute force subfolders which i added flag.txt from ~/office365/flag.txt
![image](https://github.com/user-attachments/assets/1dc27a40-b327-4958-ad9a-4b01da1d86ce)
Since the clue is fUxSVV8zSHRfaFQxd195NExwe01IVAo= it might be a base64 format so I decode it from cyberchef
![image](https://github.com/user-attachments/assets/2defffd5-92f7-4169-b79a-82e201508ca6)
The output is }LRU_3Ht_hT1w_y4Lp{MHT lets reverse it
```
THM{pL4y_w1Th_tH3_URL}
```



