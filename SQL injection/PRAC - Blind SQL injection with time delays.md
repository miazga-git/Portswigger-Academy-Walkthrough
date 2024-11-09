Title: Blind SQL injection with time delays
Level: Practitioner
Desc:  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.
To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay. 

payload: `TrackingId=l8U9GkudTF2X7jYw' || pg_sleep(10)--;`
![image](https://github.com/user-attachments/assets/529e1270-5eba-4fae-9863-af3979d318cc)
