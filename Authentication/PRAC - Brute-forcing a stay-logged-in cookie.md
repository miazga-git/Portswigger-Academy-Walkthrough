Title: Brute-forcing a stay-logged-in cookie
Level: PRACTITIONER
Desc:  This lab allows users to stay logged in even after they close their browser session. The cookie used to provide this functionality is vulnerable to brute-forcing.

To solve the lab, brute-force Carlos's cookie to gain access to his My account page.

    Your credentials: wiener:peter
    Victim's username: carlos
    Candidate passwords

# Walkthrough:
We can see : stay-logged-in cookie in response after providing correct credentials for my account.
`stay-logged-in=d2llbmVyOjUxZGMzMGRkYzQ3M2Q0M2E2MDExZTllYmJhNmNhNzcw;`

We can base64 decode this string and we get: `wiener:51dc30ddc473d43a6011e9ebba6ca770`
<img width="1079" height="537" alt="image" src="https://github.com/user-attachments/assets/13839fbe-8873-4350-8d49-94d3486b20e3" />

The second part is probably md5 hash.
<img width="1067" height="628" alt="image" src="https://github.com/user-attachments/assets/dd6b2579-ea50-4f18-9f91-ded88acc1785" />
It is md5 hash of password.

I create brute force attack on cookie using payload processing:
<img width="742" height="575" alt="image" src="https://github.com/user-attachments/assets/d9c216ca-2520-4cad-9b54-28a05b55e0f1" />

<img width="1568" height="112" alt="image" src="https://github.com/user-attachments/assets/400759fb-e731-46ba-a87f-09cfd7836963" />

We did it!
