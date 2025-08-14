Title: Username enumeration via account lock
Level: PRACTITIONER
Desc:  This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.
    Candidate usernames
    Candidate passwords

# Walkthrough: 

So, I make more than 5 the same attacks at the same time to try to send username and password, iterating through list of usernames. After touching the right account more than 5 times I get different response - account locked.

<img width="1078" height="660" alt="image" src="https://github.com/user-attachments/assets/c37a3d08-1c90-4ae9-985a-eb5015adf3f6" />

so I have username agenda.

now, bruteforcing the password - but how to do that if we have account lock mechanism.

Maybe we don't need to bypass mechanism, maybe it is vulnerable and after providing correct pair with username and password we would get redirect or something. Or maybe different error.

As I thought.
<img width="1449" height="241" alt="image" src="https://github.com/user-attachments/assets/95d7c143-c945-4e22-b527-7014e44c032d" />


<img width="628" height="277" alt="image" src="https://github.com/user-attachments/assets/7d615578-50bc-447d-a589-e20ecd61f7b4" />


