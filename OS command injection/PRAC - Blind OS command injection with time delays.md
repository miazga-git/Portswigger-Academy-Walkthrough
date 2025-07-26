Title: Blind OS command injection with time delays
Level: PRACTITIONER
Desc: This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.
To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay. 

# Walkthrough: 
The trick here was to guess what command is being run on the application side. According to portswigger blog it could be that command: 
`mail -s "This site is great" -aFrom:peter@normal-user.net feedback@vulnerable-website.com`

and now look what we control. We have form to control subject and email.

To break into subject we need payload like that : `"& ping -c 10 localhost &`. It didn't work, but I tried to add comment at the end to comment rest of the command in app: `"& ping -c 10 localhost & #`
And it worked!
<img width="1906" height="713" alt="image" src="https://github.com/user-attachments/assets/c565198a-8876-474a-b4f0-0e69ae108b7d" />
I'm not sure why sleep not working here.

According to the solution of lab it is also possible to inject command in email field: `%26+ping+-c+10+127.0.0.1+%26`


