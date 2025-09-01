Title: Authentication bypass via encryption oracle
Level: PRACTITIONER
Desc:  This lab contains a logic flaw that exposes an encryption oracle to users. To solve the lab, exploit this flaw to gain access to the admin panel and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:
We have option: "stay logged in", after clicking this option I can see cookie: `stay-logged-in=znVUEEMtXGZdYWoycRr%2f%2b5JxO3WAw8ALxq30GcVqW0E%3d;`

When I try to add invalid email address in "add comment" functionallity I get another cookie, which is encrypted: `notification=HeuiaR5bwRY%2fEzEFZUKCLSMMwaAdQskhpV9d1jrvVAk%3d;`

<img width="536" height="65" alt="image" src="https://github.com/user-attachments/assets/03ca3e76-60e6-4532-8f3e-20c6946e3e44" />
`Notice that the error message reflects your input from the email parameter in cleartext. Deduce that this must be decrypted from the notification cookie. Send the POST /post/comment and the subsequent GET /post?postId=x request (containing the notification cookie) to Burp Repeater.`

I decrypted stay-logged-in cookie providing this as a notification cookie in GET request to comment
<img width="627" height="165" alt="image" src="https://github.com/user-attachments/assets/1790e366-7f48-412a-9e83-f261f24b08e2" />

`wiener:1756743858230`

This reveals that the cookie should be in the format username:timestamp

Now I create string: `administrator:1756743858230` and I use post comment request to encrypt that.

Trying to decode cookie with administrator and timestamp in it. Deleting first 23 bytes and then reencoding the rest once again.
Then I try to add reencoded string to decoding request and I get an error.
<img width="1902" height="751" alt="image" src="https://github.com/user-attachments/assets/ef480a1c-a532-463b-af02-f3634753c200" />

<img width="892" height="144" alt="image" src="https://github.com/user-attachments/assets/d6f553b9-2be2-4394-b7ba-b207bba280d7" />

Doing the same steps but this time with padding:
xxxxxxxxxadministrator:1756743858230
In decryption and reencryption steps I delete 32 characters.

hVxM1hTE5Nj%2FYHmhHcRnmP10r2TEh%2FQ3hTOBskd46NU%3D
Now, after those operations I don't have error - invalid email address.
<img width="1054" height="390" alt="image" src="https://github.com/user-attachments/assets/ff8066d0-ca44-4f5e-8d28-d9f86d5a5704" />

```
 Go to the encrypt request and change the email parameter to administrator:your-timestamp. Send the request and then copy the new notification cookie from the response.
Decrypt this new cookie and observe that the 23-character "Invalid email address: " prefix is automatically added to any value you pass in using the email parameter. Send the notification cookie to Burp Decoder.
In Decoder, URL-decode and Base64-decode the cookie.
In Burp Repeater, switch to the message editor's "Hex" tab. Select the first 23 bytes, then right-click and select "Delete selected bytes".
Re-encode the data and copy the result into the notification cookie of the decrypt request. When you send the request, observe that an error message indicates that a block-based encryption algorithm is used and that the input length must be a multiple of 16. You need to pad the "Invalid email address: " prefix with enough bytes so that the number of bytes you will remove is a multiple of 16.

In Burp Repeater, go back to the encrypt request and add 9 characters to the start of the intended cookie value, for example:
xxxxxxxxxadministrator:your-timestamp

Encrypt this input and use the decrypt request to test that it can be successfully decrypted.
Send the new ciphertext to Decoder, then URL and Base64-decode it. This time, delete 32 bytes from the start of the data. Re-encode the data and paste it into the notification parameter in the decrypt request. Check the response to confirm that your input was successfully decrypted and, crucially, no longer contains the "Invalid email address: " prefix. You should only see administrator:your-timestamp.
From the proxy history, send the GET / request to Burp Repeater. Delete the session cookie entirely, and replace the stay-logged-in cookie with the ciphertext of your self-made cookie. Send the request. Observe that you are now logged in as the administrator and have access to the admin panel.
```
