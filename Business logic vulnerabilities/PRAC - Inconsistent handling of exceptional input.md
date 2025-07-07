Title: Inconsistent handling of exceptional input
Level: Practitioner
Desc: This lab doesn't adequately validate user input. You can exploit a logic flaw in its account registration process to gain access to administrative functionality. To solve the lab, access the admin panel and delete the user carlos. 

Walkthrough:
![image](https://github.com/user-attachments/assets/aa38cb77-0d3c-401c-be1a-b2356df5ec64)

So I could make double `@` sign in email, but I had no idea how to truncate email to only have @proper.domain.com

But I find out, that after providing email address longer than 255 chars it truncate from the last char.

So I send payload as below and app make me dontwannacry.com user.

`attackerxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx@dontwannacry.com.exploit-0aa100110493338a81dca13d01f8006a.exploit-server.net`


![image](https://github.com/user-attachments/assets/76894bf4-c328-4d54-a4ab-991eaa411b4b)

