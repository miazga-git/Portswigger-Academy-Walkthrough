Title: Authentication bypass via flawed state machine
Level: Practitioner
Desc:  This lab makes flawed assumptions about the sequence of events in the login process. To solve the lab, exploit this flaw to bypass the lab's authentication, access the admin interface, and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

Walkthrough:
during authentication I dropped second request, this one:
![image](https://github.com/user-attachments/assets/eb78980b-5bb6-40d9-8ab2-676492913112)


and it responsed with default user, which is administrator. 

So:
1. sign in as wiener: peter
2. drop request GET /role-selector
3. run request GET /admin
