# THM-Hospital-Write-Up
Hey, here you will see the write-up for Hospital machine made by “MrHex” on Tryhackme. You can access the machine from this link https://tryhackme.com/room/hospital. Let’s start!

First we are facing a message that we should add ip to hosts file on our target machine. Let’s do this and start hacking

<img width="786" height="155" alt="image" src="https://github.com/user-attachments/assets/2ebc3380-d0fc-446b-ba10-78242b84dce9" />

Edit the /etc/hosts file like this

<img width="328" height="60" alt="image" src="https://github.com/user-attachments/assets/a3564c3f-1a86-4027-94c6-ae53fadb006f" />


## When accessing the website we already know that probably here will be some IDOR (Broken Access Control) Vulnerability, from the title that we have read when starting the machine
<img width="786" height="442" alt="image" src="https://github.com/user-attachments/assets/75ba610d-84c0-48a9-be61-51160587e313" />

Website has got two main functionalities: Making an appointment and checking an appointment. Let’s make an appointment and see the request going to backend

<img width="786" height="442" alt="image" src="https://github.com/user-attachments/assets/dc8ad0f3-38b7-4cfa-9227-34ee7985120b" />

After submitting an application we get appointment_number and ID that we submitted, so let’s check the “check appointment” function

<img width="786" height="442" alt="image" src="https://github.com/user-attachments/assets/a2e47c2d-b06d-4056-bce4-0301b77010bf" />

As we see from response we get the application that we applied for however here is the main problem, backend doesn’t check if ID is binded to appointment_number so as a result we can enumerate all appointment_numbers on target machine and get information about other users

# Getting the vulnerability and reaching the flag:

<img width="786" height="603" alt="image" src="https://github.com/user-attachments/assets/74e8d354-c865-4fa5-bbf8-6297db0c839e" />

I have decided to brute force for IDs from 1 to 10000 and filtering out those that have pentest in title so I won’t see my applications

Payload:

seq 1 10000 | ffuf -w — \
-u http://hospital.thm/api/appointments/query \
-X POST \
-H “Content-Type: application/json” \
-H “Host: hospital.thm” \
-d ‘{“id_number”:”3",”appointment_number”:”APT-qZe-FUZZ-Xstr”}’ \
-fr “pentest”


<img width="786" height="442" alt="image" src="https://github.com/user-attachments/assets/850041eb-ea32-4ad2-b56f-5095037bcb92" />

And 585 was the right number of the application where we see Flag.

Thanks for Reading!




