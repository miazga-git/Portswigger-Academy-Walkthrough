Title: Parameter cloaking
Level: Practitioner
Desc:  This lab is vulnerable to web cache poisoning because it excludes a certain parameter from the cache key. There is also inconsistent parameter parsing between the cache and the back-end. A user regularly visits this site's home page using Chrome.
To solve the lab, use the parameter cloaking technique to poison the cache with a response that executes alert(1) in the victim's browser. 

# Walkthrough:
<img width="1579" height="413" alt="image" src="https://github.com/user-attachments/assets/0e2edb3e-3e48-41bd-8bd1-93151904f248" />

I saw unpopular cookie value and name of the cookie: country. So I came up on the idea to add country as a parameter in the request and I saw, that I is reflected on the response.

I send a payload, but I can see, that app is encoding special charakters.
<img width="1586" height="447" alt="image" src="https://github.com/user-attachments/assets/e88e6c7a-7480-4c9c-b279-59f773d1f94f" />

That is the place where we need to use parameter cloaking.

`?country='/><script>alert(1)</script>?country='/><script>alert(1)</script> `

I used param miner to search for additional params to try paramter cloaking.
<img width="888" height="165" alt="image" src="https://github.com/user-attachments/assets/598dc917-8601-4c95-b303-36bd41b68e34" />


I can see, that all pages use function `/js/geolocate.js?callback=setCountryCookie`
<img width="1297" height="189" alt="image" src="https://github.com/user-attachments/assets/3931ca1d-378a-4a36-a07e-28eb5bb4c391" />

<img width="1546" height="469" alt="image" src="https://github.com/user-attachments/assets/2b76cc1a-b9cc-497e-90fa-e20c14460d27" />
In the end, working payload is : `/js/geolocate.js?callback=setCountryCookie&utm_content=x;callback=xyz`

Cache see this as : /js/geolocate.js?callback=setCountryCookie  AND  &utm_content=x;callback=xyz
Especially cache see this: utm_content=x;callback=xyz as one paramter utm_content with value: x;callback=xyz

But the app see this as 3 paramters: 
callback=setCountryCookie
utm_content=x
callback=xyz

And more important is the second one.

<img width="1185" height="305" alt="image" src="https://github.com/user-attachments/assets/187333ae-e522-4809-b6ff-714bd2f07acd" />


<img width="1337" height="437" alt="image" src="https://github.com/user-attachments/assets/f1f51885-9699-470b-92dc-c8fa8d6ec9a1" />


"Alternatively, with Param Miner loaded, right-click on the request and select "Bulk scan" > "Rails parameter cloaking scan" to identify the vulnerability automatically. "
