Title: Password brute-force via password change
Level: PRACTITIONER
Desc:  This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos
    Candidate passwords

# Walkthrough: 
Observation during changing password process:

```
current pass = OK
new pass1 != new pass1 
result: New passwords do not match

current pass = !OK
new pass1 != new pass1 
result: Current password is incorrect
```

<img width="1437" height="536" alt="image" src="https://github.com/user-attachments/assets/30c36a6f-2918-490c-ab59-ef0e884b0022" />
