Title: Single-endpoint race conditions
Level: PRACTITIONER
Desc:  This lab's email change feature contains a race condition that enables you to associate an arbitrary email address with your account.

Someone with the address carlos@ginandjuice.shop has a pending invite to be an administrator for the site, but they have not yet created an account. Therefore, any user who successfully claims this address will automatically inherit admin privileges.

To solve the lab:

    Identify a race condition that lets you claim an arbitrary email address.
    Change your email address to carlos@ginandjuice.shop.
    Access the admin panel.
    Delete the user carlos

You can log in to your own account with the following credentials: wiener:peter.

You also have access to an email client, where you can view all emails sent to @exploit-<YOUR-EXPLOIT-SERVER-ID>.exploit-server.net addresses. 

# Walkthrough
I found a way (easy way) to make race condition attack on resource /my-account/change-email. I make the same requests, but 1 with my email (which can go through validation) and the 2nd one with carlos@ginandjuice.shop email, which gives me link to get this account. Because validation process is first and opens the door for a while for requests for claiming emails I can on 1 validation make 2 requests, one for my account and one for carlos account.

![image](https://github.com/user-attachments/assets/f7673c77-7077-486b-8e6e-efd8cb351170)

![image](https://github.com/user-attachments/assets/84753117-08b4-467f-b501-386df9290d81)



![image](https://github.com/user-attachments/assets/b91c82b6-590c-4fdc-b2d4-18162e843bf3)








