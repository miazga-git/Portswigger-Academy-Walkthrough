Title: Blind XXE with out-of-band interaction
Level: Practitioner
Desc:  This lab has a "Check stock" feature that parses XML input but does not display the result.
You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain.
To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator. 

Where to find collaborator in Burp:
![image](https://github.com/user-attachments/assets/c1b0b6bf-2505-4b55-bbde-5b81814eeb3d)
PRO version only 

How to check if it is potential for xxe blind: try to add entity, for example : 
`<!DOCTYPE foo [ <!ENTITY xxe SYSTEM ""> ]>`
and then try to index that entity once in proper way and once in invalid way : 

PROPER: 
![image](https://github.com/user-attachments/assets/3ddce1ba-aae7-4dd5-96c8-2a6287e83229)

INVALID: 
![image](https://github.com/user-attachments/assets/0a4490c4-350f-4c53-b939-e1d125be099b)

look: different errors
