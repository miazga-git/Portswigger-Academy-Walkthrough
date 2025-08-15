Title: Multi-step process with no access control on one step 
Level: PRACTITIONER
Desc:  This lab has an admin panel with a flawed multi-step process for changing a user's role. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.
To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator. 

# Walkthrough:
Just sending that one request:
<img width="1039" height="556" alt="image" src="https://github.com/user-attachments/assets/1dad6626-dd9f-405f-9b24-3ab47a3945b7" />

Promoting user to admin role is by 2 steps, one step require authentication as admin, second not.
