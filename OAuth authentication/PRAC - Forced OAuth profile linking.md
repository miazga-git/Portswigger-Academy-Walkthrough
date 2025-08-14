Title: Forced OAuth profile linking
Level: PRACTITIONER
Desc:  This lab gives you the option to attach a social media profile to your account so that you can log in via OAuth instead of using the normal username and password. Due to the insecure implementation of the OAuth flow by the client application, an attacker can manipulate this functionality to obtain access to other users' accounts.
To solve the lab, use a CSRF attack to attach your own social media profile to the admin user's account on the blog website, then access the admin panel and delete carlos.
The admin user will open anything you send from the exploit server and they always have an active session on the blog website.
You can log in to your own accounts using the following credentials:
    Blog website account: wiener:peter
    Social media profile: peter.wiener:hotdog

# Walkthrough:

After signing in I have option to attach my social media account:
<img width="642" height="445" alt="image" src="https://github.com/user-attachments/assets/0f9b7344-03e6-454f-b9ae-b088b5b14c2e" />


In /auth request we don't have any `state` parameter:
<img width="954" height="323" alt="image" src="https://github.com/user-attachments/assets/56c18142-effb-4769-afb8-1d46294dd748" />


Once again click: "Attach a social profile".
Intercept GET /oauth-linking?code=[...]. Copy URL.

Drop the request to make sure, that code is valid.

Creating an iframe on the exploit server: `<iframe src="https://YOUR-LAB-ID.web-security-academy.net/oauth-linking?code=STOLEN-CODE"></iframe>`

`<iframe src="https://0a1c00fd0481e9fb8019031e000d0000.web-security-academy.net/oauth-linking?code=cA8ZMaEC-vWhr1umVeFIi-qAquJB88kMRbQ_ZuKClP4"></iframe>`

Deliver the exploit to the victim. When their browser loads the iframe, it will complete the OAuth flow using your social media profile, attaching it to the admin account on the blog website.

Then try to login using social media account.

