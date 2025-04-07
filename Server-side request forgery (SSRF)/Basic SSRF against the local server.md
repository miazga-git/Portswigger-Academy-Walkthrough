Title: Basic SSRF against the local server
Desc:  This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos. 

![image](https://github.com/user-attachments/assets/d053788a-4137-456d-b49b-4db08d86283d)
So I can see, that whenever the check stock function is called, it makes call to external address. So lets, try to make call to specified in this lab special address.

```
stockApi=http%3a//localhost/admin
```

It works!
![image](https://github.com/user-attachments/assets/a5d3a69b-4d1a-4dfd-8a3e-2b3831829519)

I can see the url to delete carlos user: 

![image](https://github.com/user-attachments/assets/14434ba9-3209-4974-8fe2-e0bc51c97757)

We did it!
