Title: Web cache poisoning with multiple headers
Level: Practitioner
Desc: This lab contains a web cache poisoning vulnerability that is only exploitable when you use multiple headers to craft a malicious request. A user visits the home page roughly once a minute. To solve this lab, poison the cache with a response that executes alert(document.cookie) in the visitor's browser. 
Hint: his lab supports both the X-Forwarded-Host and X-Forwarded-Scheme headers. 

# Walkthrough:


So, there was 2 headers which combined resul in web cache attack. But it was not on the root directory of a site, but in the .js resource used by the root directory.
<img width="805" height="839" alt="image" src="https://github.com/user-attachments/assets/f1ba6374-f046-4861-9671-cbcf4343855c" />


<img width="1619" height="472" alt="image" src="https://github.com/user-attachments/assets/37b2ec3e-8322-4dba-bada-17f3955d06e6" />

Result:
<img width="1224" height="330" alt="image" src="https://github.com/user-attachments/assets/ed3d74ac-5983-4714-9445-210d2e42caf5" />
