Title: Bypassing flawed input filters for server-side prototype pollution
Level: PRACTITIONER
Desc:  This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object.
To solve the lab:
    Find a prototype pollution source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that you can use to escalate your privileges.
    Access the admin panel and delete the user carlos.
You can log in to your own account with the following credentials: wiener:peter 

# Walkthrough:
In Repeater, add a new property to the JSON with the name __proto__, containing an object with a json spaces property.
<img width="1585" height="645" alt="image" src="https://github.com/user-attachments/assets/6c7ca0fc-307a-498b-ac1d-59d3f045ce1c" />

In the Response panel, switch to the Raw tab. Observe that the JSON indentation appears to be unaffected. 

Trying to bypass filter using constructor instead of `__proto__` keyword.

```
"constructor":{"prototype": {
"json spaces":10}}
```

I can see effect of that change:
<img width="1226" height="591" alt="image" src="https://github.com/user-attachments/assets/be694415-766b-48fb-8bc6-03a424bc5117" />

changing request to escalate privilege:
<img width="1362" height="587" alt="image" src="https://github.com/user-attachments/assets/16bd1884-cc7a-4cde-a9f0-a70d9ce5f5ae" />
