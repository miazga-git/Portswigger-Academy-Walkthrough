Title: Username enumeration via response timing
Level: Practitioner
Desc:  This lab is vulnerable to username enumeration using its response times. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.
    Your credentials: wiener:peter
    Candidate usernames
    Candidate passwords

To add to the challenge, the lab also implements a form of IP-based brute-force protection. However, this can be easily bypassed by manipulating HTTP request headers. 

# Walkthrough:
After some requests trying to bruteforce login list I got alert: 
<img width="1503" height="698" alt="image" src="https://github.com/user-attachments/assets/84a14be4-82c9-4d31-a4c1-acccfade8285" />

We need to bypass this type of protection, maybe X-Forwarded-For would work. It works, but we need to change IP address in this header every 3 iterations. Not a problem :)
I found the fancy way of bypassing this protection - we don't need to have IP address in this header, we can have anything, so going through iterations of usernames, I also provide username in this header: 
<img width="1076" height="390" alt="image" src="https://github.com/user-attachments/assets/38764b01-9c63-430e-a986-b2d8c3a68ae3" />

In my way of thinking I need this tipe of attack in intruder: (buttering ram)
<img width="696" height="71" alt="image" src="https://github.com/user-attachments/assets/2716a0dc-c80b-4f69-8855-f857a1f8a1ea" />

Next trick - set the password to a very long string of characters (about 100 characters should do it). 

I found the login by response time significantly longer: 
<img width="983" height="98" alt="image" src="https://github.com/user-attachments/assets/b61eb138-47ab-4609-9110-ed597d66228c" />

login: puppet

Now bruteforcing passwords.
<img width="1360" height="455" alt="image" src="https://github.com/user-attachments/assets/4748830c-4ea9-4d32-9e1d-63466a738ff1" />

we have password.
<img width="819" height="252" alt="image" src="https://github.com/user-attachments/assets/3c0a8c31-1ba0-4209-8396-a947b90a6ed8" />


The trick here was to observe time delays in username bruteforcing, but having long password (above 100chars) in the same time.



