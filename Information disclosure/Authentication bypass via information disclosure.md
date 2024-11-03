Title: Authentication bypass via information disclosure

I found /admin directory: `https://0af60017035e8a73841fa5f500f90068.web-security-academy.net/admin`

![image](https://github.com/user-attachments/assets/8762583d-0c6c-48f8-9d9d-85f46b87a84c)

I can see, that "Admin interface only available to local users "

Using command: `curl -X TRACE "https://0af60017035e8a73841fa5f500f90068.web-security-academy.net/admin"` I can see, that
there is custom header `X-Custom-IP-Authorization: 83.24.186.73`

![image](https://github.com/user-attachments/assets/630a2236-261e-4a27-9378-8bb54e35088d)

I intercepted request to the admin panel, and I added `X-Custom-IP-Authorization: 127.0.0.1` header to the request.
![image](https://github.com/user-attachments/assets/a4213263-53f5-4416-8514-2e0095eac286)
