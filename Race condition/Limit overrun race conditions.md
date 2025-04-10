Title: Limit overrun race conditions
Desc:  This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.
To solve the lab, successfully purchase a Lightweight L33t Leather Jacket.
You can log in to your account with the following credentials: wiener:peter. 

Get request which add coupon to the cart: 
![image](https://github.com/user-attachments/assets/10f879f3-58b2-44d3-853d-897b414bc9cf)

see, that there is race condition - if you click fast "send" button multiple times you can see, that coupon code was added couple of times.

You need to use more coupons so you need to use some burp functionalities to send multiple requests in one connection.

In Repeater, add the new tab to a group.
![image](https://github.com/user-attachments/assets/3aa56116-5f3b-402d-8de8-5c7a057cc42b)

Right-click the grouped tab, then select Duplicate tab. Create 19 duplicate tabs. The new tabs are automatically added to the group. 
![image](https://github.com/user-attachments/assets/a949617f-8748-41f4-b245-66f1bf63fef2)

![image](https://github.com/user-attachments/assets/945d2475-3f9e-467c-a63a-9faef5f1c8e0)

In Repeater, send the group of requests again, but this time in parallel, effectively applying the discount code multiple times at once.

![image](https://github.com/user-attachments/assets/3b8f1284-47c2-40c1-aa08-fec79958863b)

