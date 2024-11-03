Title: URL-based access control can be circumvented
Level: Practitioner

Desc:  This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. 
However, the back-end application is built on a framework that supports the X-Original-URL header.
To solve the lab, access the admin panel and delete the user carlos. 

Need to change this:
![image](https://github.com/user-attachments/assets/5053ba36-fc4d-40e0-baec-75eb36b18c1f)

to this:
![image](https://github.com/user-attachments/assets/aa6a31fd-37f1-420a-860c-f8a2f57c91c2)

and that's all.

![image](https://github.com/user-attachments/assets/db451f80-1fbb-4831-803c-6bbbe1939e56)
