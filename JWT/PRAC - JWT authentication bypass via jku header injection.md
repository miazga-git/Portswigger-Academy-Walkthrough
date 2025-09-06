Title: JWT authentication bypass via jku header injection
Level: PRACTITIONER
Desc:  This lab uses a JWT-based mechanism for handling sessions. The server supports the jku parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.
To solve the lab, forge a JWT that gives you access to the admin panel at /admin, then delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

Tip:Instead of embedding public keys directly using the jwk header parameter, some servers let you use the jku (JWK Set URL) header parameter to reference a JWK Set containing the key. When verifying the signature, the server fetches the relevant key from this URL. A JWK Set is a JSON object containing an array of JWKs representing different keys.
Tip2: JWK Sets like this are sometimes exposed publicly via a standard endpoint, such as /.well-known/jwks.json. 

# Walkthrough:
In Burp, load the JWT Editor extension from the BApp store. 

Go to the JWT Editor Keys tab in Burp's main tab bar. 

Click new rsa key and generate key pair.

In the browser, go to the exploit server. 

Copy public key from pair recently created (jwk format):
<img width="1810" height="384" alt="image" src="https://github.com/user-attachments/assets/439f8181-0347-4670-b389-6b406f1edc29" />


Store public key on the exploit server: 
<img width="1528" height="839" alt="image" src="https://github.com/user-attachments/assets/6a12b9c6-e658-4aff-bb59-bc16184adeed" />

Go back to the GET /admin request in Burp Repeater and switch to the extension-generated JSON Web Token message editor tab. 

In the header of the JWT, replace the current value of the kid parameter with the kid of the JWK that you uploaded to the exploit server. 
Add a new jku parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server. 
In the payload, change the value of the sub claim to administrator. 
At the bottom of the tab, click Sign, then select the RSA key that you generated in the previous section. 
Make sure that the Don't modify header option is selected, then click OK. The modified token is now signed with the correct signature. 

<img width="1099" height="740" alt="image" src="https://github.com/user-attachments/assets/9867bdca-ff34-4df9-a019-5acd992328f6" />
