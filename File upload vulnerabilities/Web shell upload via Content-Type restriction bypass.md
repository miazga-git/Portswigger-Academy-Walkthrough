Desc: This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this. 

![image](https://github.com/user-attachments/assets/c23c9271-7691-4178-916d-cda5563c0a1f)
"Sorry, file type application/x-php is not allowed Only image/jpeg and image/png are allowed Sorry, there was an error uploading your file."

![image](https://github.com/user-attachments/assets/8f34abfb-6439-43b9-8819-4d817ead7f7f)
![image](https://github.com/user-attachments/assets/8835f19e-d1ce-413a-8bfe-344808324904)
So it is possible to intercept request uploading png file and change extension to php during intercepting.


URL to attack: `https://0a6700b6046a225a80176cf8002e0068.web-security-academy.net/files/avatars/webshell.php?cmd=cat+/home/carlos/secret`

Another way to do this:
1) Intercept the request:
![image](https://github.com/user-attachments/assets/0864bf58-e505-4dfd-ba51-829afb664912)

2) Change Content-Type to "legal" one (e.g. `Content-Type: image/png`):
![image](https://github.com/user-attachments/assets/0656b68c-20d7-4b2c-a742-0860087c045d)


