Title: JWT authentication bypass via jwk header injection
Level: Practitioner 
Desc:  This lab uses a JWT-based mechanism for handling sessions. The server supports the jwk parameter in the JWT header. This is sometimes used to embed the correct verification key directly in the token. However, it fails to check whether the provided key came from a trusted source.
To solve the lab, modify and sign a JWT that gives you access to the admin panel at /admin, then delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 


![image](https://github.com/user-attachments/assets/d26e42dc-e83a-4dea-8d0f-8549336a476d)

![image](https://github.com/user-attachments/assets/bdabd0e4-e199-4285-827e-33d48887ccb7)


How to attack JWT token with jwk parameter: 
# attempt 1 - use Burpsuite Extension
Here you can create key - please remember to create key with proper algoritm (can be symethric or asymethric)
![image](https://github.com/user-attachments/assets/118e6276-e941-4433-84ca-bc05e7b3035a)

![image](https://github.com/user-attachments/assets/396b1c09-91af-4930-8baf-5591acfd674a)

In the repeater you can find jwt plugin, which gives possibility to make some attack on jwt token, including attacks on jwk parameter:
![image](https://github.com/user-attachments/assets/899a6e1d-bf13-47a9-ae46-24ad846155d2)

Attack - embedded jwk - use created key to sign jwt token
Before that change payload to meet your goals - in my case it was changing sub to administrator

Forged token: 
![image](https://github.com/user-attachments/assets/08af94a6-468e-4c7c-965e-23747d337cb4)

click send to check out if token is valid.











