Title: Web cache poisoning with an unkeyed cookie
Level: Practitioner
Desc: This lab is vulnerable to web cache poisoning because cookies aren't included in the cache key. An unsuspecting user regularly visits the site's home page. To solve this lab, poison the cache with a response that executes alert(1) in the visitor's browser. 

# Walkthrough:
My cookie is reflected in response and also I can try from different "session" to make request to root directory of site and I can see, that response comes from cache and it contains the same string as in the cookie.

<img width="1518" height="340" alt="image" src="https://github.com/user-attachments/assets/2b9ebee1-6e96-48f6-a304-8fc1a722829d" />


<img width="986" height="408" alt="image" src="https://github.com/user-attachments/assets/62d6bc33-8467-4619-973c-676e19715f1d" />


Now I need to create payload to execute code: `miazga"}%3balert(1)%3bdata2%3d{"x"%3a"`

<img width="1415" height="704" alt="image" src="https://github.com/user-attachments/assets/3d17e1ba-b193-48ae-a3e1-2b5dfcf649f7" />


<img width="1433" height="276" alt="image" src="https://github.com/user-attachments/assets/0bfdb705-bb1b-4e47-b185-716d8b155c66" />
