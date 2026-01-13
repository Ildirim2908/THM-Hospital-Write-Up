# THM-Hospital-Write-Up
Hey, here you will see the write-up for Hospital machine made by “MrHex” on Tryhackme. You can access the machine from this link https://tryhackme.com/room/hospital. Let’s start!

First we are facing a message that we should add ip to hosts file on our target machine. Let’s do this and start hacking

<img width="786" height="155" alt="image" src="https://github.com/user-attachments/assets/2ebc3380-d0fc-446b-ba10-78242b84dce9" />

Edit the /etc/hosts file like this
<img width="328" height="60" alt="image" src="https://github.com/user-attachments/assets/a3564c3f-1a86-4027-94c6-ae53fadb006f" />
When accessing the website we already know that probably here will be some IDOR (Broken Access Control) Vulnerability, from the title that we have read when starting the machine
<img width="786" height="442" alt="image" src="https://github.com/user-attachments/assets/75ba610d-84c0-48a9-be61-51160587e313" />


