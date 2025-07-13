Title: Web cache poisoning with an unkeyed header
Level: Practitioner
Desc: This lab is vulnerable to web cache poisoning because it handles input from an unkeyed header in an unsafe way. An unsuspecting user regularly visits the site's home page. To solve this lab, poison the cache with a response that executes alert(document.cookie) in the visitor's browser. 

# Walkthrough:
I found out, that I can add `X-Forwarded-Host: xyz` header and value of this header is reflected to the response from server.
<img width="1495" height="399" alt="image" src="https://github.com/user-attachments/assets/a70bc166-83c4-44e7-9baa-e5f707d190ab" />

I try to make request to / of site and I got response from cache containing vlaued added via X-Forwarded-Host header.
<img width="1010" height="427" alt="image" src="https://github.com/user-attachments/assets/0347cb7a-ae07-462b-88ae-c3fa051cf1a0" />

Now as a value I need to use : `"></script><script>alert(document.cookie)</script><script type="text/javascript" src="/`


<img width="1233" height="316" alt="image" src="https://github.com/user-attachments/assets/464bd4d3-fd35-4124-9ecf-7e3bf82215da" />

