Title: 2FA simple bypass
Desc:  This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.
    Your credentials: wiener:peter
    Victim's credentials carlos:montoya

Basically, to get our account we need to send 3 request:
First request to "/login"
![image](https://github.com/user-attachments/assets/13cd223d-a432-430c-9986-a1f8782833ab)
Here our session is changed, for example we start with cookie: V9bExZrs3d5DYZikuTLeisM1M0KbqTbx and we get redirection and another cookie: 
lb4GNsZZA1eK2YdOSWgsTr1mmzFvf5XN

Second request goes to the "/login2", here we are asked to provide second factor code.
![image](https://github.com/user-attachments/assets/8e17150f-129c-4fb7-81a0-53d7aa739b58)
Here our session  is changed once again and we get redirection to the "/my-account?id=wiener" 
`/my-account?id=<username>`

![image](https://github.com/user-attachments/assets/dc63e76e-6387-442d-9783-756aa84ed8e3)

How to get carlos account?
1. login in with provided credentials
2. look - your session has been changed, write that session cookie
3. try to send GET request to `/my-account?id=<username>` providing session from step 2.
4. You are IN!








