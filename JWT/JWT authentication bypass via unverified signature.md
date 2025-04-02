Title: JWT authentication bypass via unverified signature
Desc:  This lab uses a JWT-based mechanism for handling sessions. Due to implementation flaws, the server doesn't verify the signature of any JWTs that it receives.
To solve the lab, modify your session token to gain access to the admin panel at /admin, then delete the user carlos.

First go to login page and log in as wiener - you have credentials for that.

Check out the session cookie - it is JWT token 

Try to decode it - for example here https://token.dev/

change payload to look like payload for user administrator: 

![image](https://github.com/user-attachments/assets/249b6a9d-5cfc-47f3-af2f-e6dead3e432d)

Here you go!

