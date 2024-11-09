Ttile: File path traversal, traversal sequences blocked with absolute path bypass
Level: Practitioner
Desc:  This lab contains a path traversal vulnerability in the display of product images.
The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory.
To solve the lab, retrieve the contents of the /etc/passwd file. 

After loading / page: 
![image](https://github.com/user-attachments/assets/cf567694-35c0-4a8d-ab77-20ab4d14ed3a)

So we have point of entry.

According to the "The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory. ", I think, that app should block payloads like that: `/etc/passwd`,
however it should not block payload like that: `../../../../../../etc/passwd`

Let's check
![image](https://github.com/user-attachments/assets/e16d9456-9ae3-487f-b4f3-dbd5f5d7e38b)

No such file, maybe I need to use exact number of directories - I tried but I got no results anyway.

I managed to find solution, so the absolute path is possible: 
![image](https://github.com/user-attachments/assets/8d51a7b2-d2b3-47a4-8111-8c518e7c21d0)
payload: `/image?filename=/etc/passwd`
