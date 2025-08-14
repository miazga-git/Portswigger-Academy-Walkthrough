Title: Password reset poisoning via middleware
Level: PRACTITIONER
Desc: This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. 
To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: wiener:peter. 
Any emails sent to this account can be read via the email client on the exploit server. 

# Walkthrough: 
During reset of password for account there is a POST request. In this request we can use X-Forwarded-For to point to specified domain, which we control.
<img width="1041" height="445" alt="image" src="https://github.com/user-attachments/assets/9d990767-f968-44a8-825b-b7a20d405cc0" />

And after that we will get email like that: 
<img width="1363" height="327" alt="image" src="https://github.com/user-attachments/assets/4bae82d2-5d7b-4401-9bff-74f8566b0cca" />

Now I will change user to carlos to get his token and then I will reconstruct the link to be valid. We know, that carlos would click the link so his reset token we should find in logs in our server.
<img width="731" height="488" alt="image" src="https://github.com/user-attachments/assets/ad8149ad-454e-4aec-a786-334c045d4f06" />

`/forgot-password?temp-forgot-password-token=axyvpze91k8ewfcf41p9rhx0z2j216ba`

<img width="1213" height="459" alt="image" src="https://github.com/user-attachments/assets/a78b67d0-62c3-46b9-959d-90ced0b2ecc4" />

