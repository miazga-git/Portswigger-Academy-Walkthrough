Title: Broken brute-force protection, IP block
Level: PRACTITIONER
Desc:  This lab is vulnerable due to a logic flaw in its password brute-force protection. To solve the lab, brute-force the victim's password, then log in and access their account page.

    Your credentials: wiener:peter
    Victim's username: carlos
    Candidate passwords


# Walkthrough: 

The trick here:  However, notice that you can reset the counter for the number of failed login attempts by logging in to your own account before this limit is reached. 
So I can send 2 request for bruteforce attack, then I need to make 1 request for my account (successful) and then I can add 2 more request for bruteforce need and so on..

Now I just need to automate that.

pitchfork attack in intruder.

<img width="1122" height="451" alt="image" src="https://github.com/user-attachments/assets/3d5853c4-2db2-4fbc-91d6-0304c7a7f73e" />
