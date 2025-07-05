Title: Basic server-side template injection
Level: Practitioner
Desc:  
This lab is vulnerable to server-side template injection due to the unsafe construction of an ERB template.
To solve the lab, review the ERB documentation to find out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory. 

Walkthrough:
First you need to see, that first item in the shop gives other response than the rest.

![image](https://github.com/user-attachments/assets/32f9ab43-aabc-48de-ad6a-6c51c2c3a4df)

So we know, that application handle GET request to resource: `/?message=Unfortunately this product is out of stock`
Next - I assume, that message is our input for SSTI payload.

I try many SSTI basic test paylads and I find out, that this one works well: `<%= 3 * 3 %>`
It is Embedded Ruby (ERB) template.

Now I can modify my payload according to the documentation of ERB to firstly list files in working directory and then to delete file from description.

![image](https://github.com/user-attachments/assets/89986e0c-08b3-4082-b493-b045880379d9)

![image](https://github.com/user-attachments/assets/5d3ccfcd-5053-4720-95e7-b74428b6e361)

