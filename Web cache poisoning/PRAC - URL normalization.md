Title: URL normalization
Level: Practitioner
Desc:  This lab contains an XSS vulnerability that is not directly exploitable due to browser URL-encoding.
To solve the lab, take advantage of the cache's normalization process to exploit this vulnerability. Find the XSS vulnerability and inject a payload that will execute alert(1) in the victim's browser. Then, deliver the malicious URL to the victim. 

# Walkthrough:
I found the entrance, place for injection.
<img width="1366" height="754" alt="image" src="https://github.com/user-attachments/assets/09571939-b410-47b5-98d6-e286e8d8051d" />

My payload is encoded by the app:
<img width="1554" height="691" alt="image" src="https://github.com/user-attachments/assets/2f009cbb-8370-4601-af69-8ab0a4c93f92" />

I can also impact another url, in fact any random path: 
<img width="1245" height="403" alt="image" src="https://github.com/user-attachments/assets/d60ad53e-c0a8-47d5-b7d2-54d2b20e8444" />

Request using payload:
<img width="1424" height="426" alt="image" src="https://github.com/user-attachments/assets/048b4f56-9a3e-41e6-88e7-66b5c6d814d9" />

`Notice that if you request this URL in the browser, the payload doesn't execute because it is URL-encoded. `
<img width="975" height="91" alt="image" src="https://github.com/user-attachments/assets/77b8ebfc-8e57-407b-8484-5232d361b3a8" />

I need to immedietly go to link in browser and it is loaded as XSS
<img width="1371" height="300" alt="image" src="https://github.com/user-attachments/assets/3163a345-6d96-43dc-97cc-1e805f72532a" />

