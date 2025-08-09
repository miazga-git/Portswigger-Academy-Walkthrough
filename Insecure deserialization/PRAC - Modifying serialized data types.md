Title: Modifying serialized data types
Level: PRACTITIONER
Desc: This lab uses a serialization-based session mechanism and is vulnerable to authentication bypass as a result. To solve the lab, edit the serialized object in the session cookie to access the administrator account. Then, delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter 

Hint: To access another user's account, you will need to exploit a quirk in how PHP compares data of different types.
Note that PHP's comparison behavior differs between versions. This lab assumes behavior consistent with PHP 7.x and earlier.

# Theory:
In PHP v7. comparison like that results in TRUE: 0 == "something" 

# Walkthrough:

Cookie for my wiener user is encoded in base64 and after decoding I can see:
```
O:4:"User":2:{s:8:"username";s:6:"wiener";s:12:"access_token";i:32:"uoc930v6r3fwpsx45ocm0evszxs4wtm0";}
```

I change this string to `O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}` .
I decided to try to provide 0 as access_token and it's type is integer instead of string, so now during comparison provided 0 and some access_token as string I should always get TRUE.
I also changed user to administrator.

I need to encode by base64 and the url encode followed string and use this in requests.

*However I did everything as in solution but in my case lab was not working.*





