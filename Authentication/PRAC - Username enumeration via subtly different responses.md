Title: Username enumeration via subtly different responses
Level: PRACTITIONER
Desc:  This lab is subtly vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:
    Candidate usernames
    Candidate passwords
To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

# Walkthrough: 

I used intruder to make brute force using login list. I make flag to detect string : "Invalid username or password."
As occured, one of the responses didn't have "." at the end and it is probably indicator of username being used.

<img width="1312" height="458" alt="image" src="https://github.com/user-attachments/assets/8637989e-20c8-47d7-bb85-ebcd357d413d" />

username: al

bruteforcing also password: 
<img width="832" height="422" alt="image" src="https://github.com/user-attachments/assets/8d847428-1af8-4a6c-b8e3-7b33c87e3529" />

<img width="439" height="213" alt="image" src="https://github.com/user-attachments/assets/b6e408f8-3a0f-4a0d-8f27-02b101d10522" />

