Title: Detecting server-side prototype pollution without polluted property reflection
Level: PRACTITIONER
Desc:  This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object.
To solve the lab, confirm the vulnerability by polluting Object.prototype in a way that triggers a noticeable but non-destructive change in the server's behavior. As this lab is designed to help you practice non-destructive detection techniques, you don't need to progress to exploitation.
You can log in to your own account with the following credentials: wiener:peter 

# Walkthrough:
<img width="1187" height="521" alt="image" src="https://github.com/user-attachments/assets/fc118b58-fb60-4ca1-9e00-aa472acaed83" />

Send the request. Observe that the object in the response does not reflect the injected property. However, this doesn't necessarily mean that the application isn't vulnerable to prototype pollution.


Changing the body in request to cause an error: 
<img width="1629" height="555" alt="image" src="https://github.com/user-attachments/assets/37b175f1-2ba6-4a20-a6e7-8e01e44118fb" />
Notice that although you received a 500 error response, the error object contains a status property with the value 400

I changed payload to: 
```
"__proto__":{
"status":"499"}
```

and after causing error again I can see, that we have another status code.

