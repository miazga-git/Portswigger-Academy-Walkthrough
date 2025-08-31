Title: SQL injection with filter bypass via XML encoding
Level: PRACTITIONER
Desc:  This lab contains a SQL injection vulnerability in its stock check feature. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables.
The database contains a users table, which contains the usernames and passwords of registered users. To solve the lab, perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account. 

# Walkthrough:
A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack. You'll need to find a way to obfuscate your malicious query to bypass this filter. We recommend using the Hackvertor extension to do this. 

We have filtering of dangerous strings provided in body of a request: 
<img width="1268" height="542" alt="image" src="https://github.com/user-attachments/assets/2dab7ae5-abe5-44f1-ba86-227d74241a2f" />

Installing plugin `hackvertor` to my burpsuite.

How to use hackvertor plugin to encode my request with sqli in it : Just highlight your input, right-click, then select Extensions > Hackvertor > Encode > dec_entities/hex_entities. 

<img width="1191" height="494" alt="image" src="https://github.com/user-attachments/assets/89d02f75-d99d-481a-9310-22d6814de1ab" />

Now I got my response back, so my payload thanks to encoding with `hackvertor` is no longer blocked.

Pick up where you left off, and deduce that the query returns a single column. When you try to return more than one column, the application returns 0 units, implying an error. 

Sending request with that body: 
```
<?xml version="1.0" encoding="UTF-8"?><stockCheck><productId>1</productId><storeId><@hex_entities>1 UNION SELECT username || password FROM users where username='administrator'</@hex_entities></storeId></stockCheck>
```

<img width="1292" height="554" alt="image" src="https://github.com/user-attachments/assets/563f6508-6a01-4de0-91d2-5020e4178210" />
