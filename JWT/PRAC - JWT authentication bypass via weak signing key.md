Title: JWT authentication bypass via weak signing key
Level: PRACTITIONER
Desc:  This lab uses a JWT-based mechanism for handling sessions. It uses an extremely weak secret key to both sign and verify tokens. This can be easily brute-forced using a wordlist of common secrets.
To solve the lab, first brute-force the website's secret key. Once you've obtained this, use it to sign a modified session token that gives you access to the admin panel at /admin, then delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

How to pass:
First of all I log in using provided credentials and then I receive token: eyJraWQiOiJmZDUzMzBlOC05ZDJiLTRkN2QtYTZhZC0wY2U3MGU0MmU1YzgiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzQ0OTk5NSwic3ViIjoid2llbmVyIn0.O7x0beouFqvj7d98EOkp7BhD76rVuW4MFdNL_cRgFaM

I check the algorithm and I can see that we have here HS256
![image](https://github.com/user-attachments/assets/11c5488c-4b0c-489d-9386-d8a597a111e1)


Let's try to crack jwt secret used for signing jwt token:
`hashcat -m 16500 -a 0 jwt_hash.txt wordlist.txt`
jwt_hash.txt - please add complete hash, not part of it

![image](https://github.com/user-attachments/assets/136f6f6f-b167-47b1-8f95-8e0c34d998fa)

so, we have secret! 

Now we can try to create and sign our own jwt token and we can sign it.
please note: jwt.io is better for signing jwt and creating forged jwt token:
![image](https://github.com/user-attachments/assets/75b4212e-abd2-4177-8c22-845bdbfd070c)




