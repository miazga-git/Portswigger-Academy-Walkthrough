Title: Host header authentication bypass
Desc:  This lab makes an assumption about the privilege level of the user based on the HTTP Host header.
To solve the lab, access the admin panel and delete the user carlos. 

The description says about admin panel, so I have found the /admin endpoint, when I try to get there I can see: Admin interface only available to local users

So let's try to use Host Header injection and instead of classic domain let's use localhost.

![image](https://github.com/user-attachments/assets/6728bcca-db7e-4fc0-a61f-d30819069ae6)

whoah it works!

![image](https://github.com/user-attachments/assets/419022d2-2742-4e5f-aa86-780df6afa5dd)



