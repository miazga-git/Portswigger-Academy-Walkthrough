Title: Weak isolation on dual-use endpoint
Level: Practitioner
Desc:  This lab makes a flawed assumption about the user's privilege level based on their input. As a result, you can exploit the logic of its account management features to gain access to arbitrary users' accounts. To solve the lab, access the administrator account and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

Walkthrough:
I send request to change password.
![image](https://github.com/user-attachments/assets/47cb6ff9-c4b5-472d-9c00-0e50d5fc9934)

I change request to this: I deleted current password parameter and also I changed user to administrator
![image](https://github.com/user-attachments/assets/d2380887-7765-4380-a2c7-b689d496f44f)
