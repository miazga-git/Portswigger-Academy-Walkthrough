Title: JWT authentication bypass via kid header path traversal
Level: PRACTITIONER
Desc:  This lab uses a JWT-based mechanism for handling sessions. In order to verify the signature, the server uses the kid parameter in JWT header to fetch the relevant key from its filesystem.
To solve the lab, forge a JWT that gives you access to the admin panel at /admin, then delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 


# Walkthrough:

Generate new symmetric key and replace the generated value for the k property with a Base64-encoded null byte (AA==). 

<img width="1389" height="723" alt="image" src="https://github.com/user-attachments/assets/50c54ae9-c4c8-497d-8209-f047b1d37e24" />

Signing jwt token with key created using null byte and in kid we point to /dev/null file in linux
<img width="1328" height="780" alt="image" src="https://github.com/user-attachments/assets/8eb9cc01-b21d-49ae-9161-82bc109ccc90" />

afer sending requet we have admin user.
