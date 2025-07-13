Title: Web cache poisoning via a fat GET request
Level: Practitioner
Desc:  This lab is vulnerable to web cache poisoning. It accepts GET requests that have a body, but does not include the body in the cache key. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the cache with a response that executes alert(1) in the victim's browser. 

# Walkthrough:

I made fat GET request with body: `callback=abc` and it is reflected on the response.
<img width="1233" height="461" alt="image" src="https://github.com/user-attachments/assets/9b2b9fca-dbde-4092-b501-99162c6fcf02" />

<img width="1471" height="483" alt="image" src="https://github.com/user-attachments/assets/c1574243-1f45-4002-a041-37aed0400d7e" />


<img width="1355" height="411" alt="image" src="https://github.com/user-attachments/assets/413de0dd-bf02-469e-950a-a79386360890" />
