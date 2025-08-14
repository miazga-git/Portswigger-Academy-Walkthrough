Title: Accidental exposure of private GraphQL fields
Level: PRACTITIONER
Desc:  The user management functions for this lab are powered by a GraphQL endpoint. The lab contains an access control vulnerability whereby you can induce the API to reveal user credential fields.
To solve the lab, sign in as the administrator and delete the username carlos.
Learn more about Working with GraphQL in Burp Suite. 

# Walkthrough:
I can see, that app introduce request to /graphql/v1
<img width="1346" height="616" alt="image" src="https://github.com/user-attachments/assets/0418e8ed-f2a7-4360-b82e-31abcccc176a" />

I used trick in Burp to make introspection query:
<img width="1134" height="692" alt="image" src="https://github.com/user-attachments/assets/2a04d768-2295-4049-918e-3ba3402aa880" />

used this tool http://nathanrandal.com/graphql-visualizer/ to paste response from graphql.

<img width="1773" height="871" alt="image" src="https://github.com/user-attachments/assets/4d9c33c4-95db-4a8e-b2c0-ec884539d8f4" />

```
{"query":"{getUser(id: 1) {id username password}}"}
```
<img width="1125" height="445" alt="image" src="https://github.com/user-attachments/assets/47e74f05-efdc-41e0-8c46-2e116eee1441" />

