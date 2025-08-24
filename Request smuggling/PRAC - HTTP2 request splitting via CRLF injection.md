Title: HTTP/2 request splitting via CRLF injection
Level: PRACTITIONER
Desc:  This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests and fails to adequately sanitize incoming headers.
To solve the lab, delete the user carlos by using response queue poisoning to break into the admin panel at /admin. An admin user will log in approximately every 10 seconds.
The connection to the back-end is reset every 10 requests, so don't worry if you get it into a bad state - just send a few normal requests to get a fresh connection. 

# Walkthrough:
<img width="1878" height="739" alt="image" src="https://github.com/user-attachments/assets/29765655-35e5-4f0a-a965-80d47128c073" />

After desynchronising the queue I finally get 302 response dedicated for admin user:
<img width="1440" height="238" alt="image" src="https://github.com/user-attachments/assets/1774d240-1953-41c3-bfbf-337f83aa14c1" />

session: `0ESU9Pj0Ln4mN9XMhNeIEBzMvLVjq661`
