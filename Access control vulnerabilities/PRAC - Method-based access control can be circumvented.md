Title: Method-based access control can be circumvented
Level: Practitioner
Desc:  This lab implements access controls based partly on the HTTP method of requests. You can familiarize yourself with the admin panel
by logging in using the credentials administrator:admin.
To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator. 


![image](https://github.com/user-attachments/assets/a3931c5d-b634-4d70-b053-896bf30bb02b)

![image](https://github.com/user-attachments/assets/01e57d49-9b82-461f-b16a-851f2b126c10)

CHANGE REQUEST METHOD in repeater in Burp
![image](https://github.com/user-attachments/assets/99a6248a-abc1-491f-b55d-5af7b558fe74)

Validation based on privileges and roles was in standard POST request, but there wasn't in GET request.
