Title: Reflected XSS into HTML context with most tags and attributes blocked
Level: Practitioner
Desc:  This lab contains a reflected XSS vulnerability in the search functionality but uses a web application firewall (WAF) to protect against common XSS vectors.
To solve the lab, perform a cross-site scripting attack that bypasses the WAF and calls the print() function. 


payload: `'<script>print()</script>`
![image](https://github.com/user-attachments/assets/17b844a2-9410-40b8-a8ff-bb4b74f5fb5c)

We have injection between <h1></h1> tags so if we test payloads it is only resonable to tests peyloads within <>,
so in in truder configuration should look like that:
![image](https://github.com/user-attachments/assets/2c45f663-69bc-4d96-8401-d731af5e6da6)


step II: Visit the XSS cheat sheet and click Copy tags to clipboard. 
step III: In the Payloads side panel, under Payload configuration, click Paste to paste the list of tags into the payloads list. Click Start attack.

step IV: Dla <body> mamy 200

step V: create intruder attack using <body%20&&=1> TAG
![image](https://github.com/user-attachments/assets/0d4c0942-b28f-4927-a2dc-4b85ea3a77c1)

step VI: Visit the XSS cheat sheet and click Copy events to clipboard. 
step VII: In the Payloads side panel, under Payload configuration, click Clear to remove the previous payloads. Then click Paste to paste the list of attributes into the payloads list. Click Start attack. 

payloadd `/?search=<body%20onresize=1>` is working

ATTACK server: `<iframe src="https://YOUR-LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'>`


