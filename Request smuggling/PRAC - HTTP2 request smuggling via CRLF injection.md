Title: HTTP/2 request smuggling via CRLF injection
Level: PRACTITIONER
Desc:  This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests and fails to adequately sanitize incoming headers.
To solve the lab, use an HTTP/2-exclusive request smuggling vector to gain access to another user's account. The victim accesses the home page every 15 seconds.
If you're not familiar with Burp's exclusive features for HTTP/2 testing, please refer to the documentation for details on how to use them. 


Some hints:
```
 To force Burp Repeater to use HTTP/2 so that you can test for this misconfiguration manually:

    From the Settings dialog, go to Tools > Repeater.
    Under Connections, enable the Allow HTTP/2 ALPN override option.
    In Repeater, go to the Inspector panel and expand the Request attributes section.
    Use the switch to set the Protocol to HTTP/2. Burp will now send all requests on this tab using HTTP/2, regardless of whether the server advertises support for this.
```

and:
In HTTP2 it is possible to send: `Foo: bar\nTransfer-Encoding: chunked`

and:
`To inject newlines into HTTP/2 headers, use the Inspector to drill down into the header, then press the Shift + Return keys. Note that this feature is not available when you double-click on the header. `

# Walkthrough
My search history is tied to session cookie.

Make sure, that protocol is HTTP/2.

How to add `Foo:bar\n\rTransfer-Encoding: chunked` to request in Burp:
<img width="1899" height="809" alt="image" src="https://github.com/user-attachments/assets/bdb968bf-feee-49e0-80c1-2d841dd6385b" />

Every second request is not found now:
<img width="1539" height="321" alt="image" src="https://github.com/user-attachments/assets/25f1f17c-f87d-47be-9e2f-6901ea9608cc" />


Now I send this request:
<img width="830" height="431" alt="image" src="https://github.com/user-attachments/assets/93470838-a177-4da0-b4b5-74e8e50fbac2" />
Now, when I try to refresh the page I get this: 
<img width="1106" height="696" alt="image" src="https://github.com/user-attachments/assets/1cef4a6b-ad17-456a-b6ce-28942995ede1" />

So my GET request was added to search=x from smuggled request. Now i can try to refresh page and check for recent searches.

After waiting 15seconds for victim request I refresh home page and in search history I can see victim's cookie. 
<img width="805" height="285" alt="image" src="https://github.com/user-attachments/assets/a2f6fc67-ea5e-4646-980e-28e56e5c2fe4" />




