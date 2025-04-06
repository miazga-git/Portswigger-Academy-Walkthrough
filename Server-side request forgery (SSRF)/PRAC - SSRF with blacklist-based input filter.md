Title: SSRF with blacklist-based input filter
Level: Practitioner
Desc:  This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.
The developer has deployed two weak anti-SSRF defenses that you will need to bypass. 

![image](https://github.com/user-attachments/assets/d789157a-d664-43d8-9c86-18ca9a1a1b9c)

error: "External stock check blocked for security reasons"

trying to use http://127.1 to bypass security:
![image](https://github.com/user-attachments/assets/a4360bac-ad60-4237-b3f0-675f3e58a98b)

it worked:
`stockApi=http%3a//127.1/aDmin`

![image](https://github.com/user-attachments/assets/83335b03-57dd-40ed-a290-4b236dfa0828)


![image](https://github.com/user-attachments/assets/13082a2f-49f6-4247-a38b-94e80f9c8ed7)

in solution they say to double url encode 'a' letter in "admin" phrase but changing lower to upper case helped in my case.
