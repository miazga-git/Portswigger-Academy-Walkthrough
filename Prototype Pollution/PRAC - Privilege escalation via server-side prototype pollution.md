Title: Privilege escalation via server-side prototype pollution
Level: PRACTITIONER
Desc:  This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object. This is simple to detect because any polluted properties inherited via the prototype chain are visible in an HTTP response.
To solve the lab:
    Find a prototype pollution source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that you can use to escalate your privileges.
    Access the admin panel and delete the user carlos.
You can log in to your own account with the following credentials: wiener:peter 

# Walkthrough:
<img width="1052" height="556" alt="image" src="https://github.com/user-attachments/assets/886a53f8-305d-45b7-9aba-46dec00fb20d" />

Adding:
```
"__proto__": {
    "foo":"bar"
}
```

<img width="1087" height="604" alt="image" src="https://github.com/user-attachments/assets/b453571b-b732-448f-8e56-31cbcc87b2e6" />


<img width="900" height="548" alt="image" src="https://github.com/user-attachments/assets/c6da6517-8bd9-4580-a672-bbacc26b67e6" />



