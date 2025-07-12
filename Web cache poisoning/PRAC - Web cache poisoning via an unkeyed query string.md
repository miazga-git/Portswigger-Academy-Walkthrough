Title: Web cache poisoning via an unkeyed query string
Level: Practitioner
Desc:  This lab is vulnerable to web cache poisoning because the query string is unkeyed. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the home page with a response that executes alert(1) in the victim's browser. 

Hint: If you're struggling, you can use the Pragma: x-get-cache-key header to display the cache key in the response. This applies to some of the other labs as well. 

# Walkthrough: 
From the hint section I see, that I can use : `Pragma: x-get-cache-ke` header and using it I can see, that app doesn't use parameters in GET request as cache key

What is more, I can see, that after making request GET /?abcd and storing it in cache I get response with abcd even if I make GET /?a :
<img width="1580" height="396" alt="image" src="https://github.com/user-attachments/assets/c6654bf2-3746-4d2a-955b-9f6ed4ae49cd" />

So my parameters are stored in cache response, but are not cache keys.

I can try to use parameter: `/?abcde='/><script>alert(1)</script>` and I can see, that it is reflected in response as a proper XSS attack.

<img width="1564" height="493" alt="image" src="https://github.com/user-attachments/assets/d16f64b4-6b1c-4b78-bde5-7276ddfa1ce3" />



