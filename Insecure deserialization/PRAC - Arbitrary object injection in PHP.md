Title: Arbitrary object injection in PHP
Level: PRACTITIONER
Desc: This lab uses a serialization-based session mechanism and is vulnerable to arbitrary object injection as a result. To solve the lab, create and inject a malicious serialized object to delete the morale.txt file from Carlos's home directory. You will need to obtain source code access to solve this lab. 
Hint: You can sometimes read source code by appending a tilde (~) to a filename to retrieve an editor-generated backup file. 

# Walkthrough:
I can see, that site references some libs resource:
<img width="904" height="523" alt="image" src="https://github.com/user-attachments/assets/ed9c6aaf-6768-4c42-bbb5-7ad24868fd40" />

I added `~` sign to get documentation of /libs/CustomTemplate.php~
<img width="1190" height="669" alt="image" src="https://github.com/user-attachments/assets/ab7dd14b-40ae-45f8-97d3-f0ea7a8200c1" />

"In the source code, notice the CustomTemplate class contains the __destruct() magic method. This will invoke the unlink() method on the lock_file_path attribute, which will delete the file on this path. "

<img width="1041" height="736" alt="image" src="https://github.com/user-attachments/assets/a6792aab-06f1-436e-a743-22f04365160b" />

"In Burp Decoder, use the correct syntax for serialized PHP data to create a CustomTemplate object with the lock_file_path attribute set to /home/carlos/morale.txt. Make sure to use the correct data type labels and length indicators. The final object should look like this: "

`O:14:"CustomTemplate":1:{s:14:"lock_file_path";s:23:"/home/carlos/morale.txt";}`

Base64 and URL-encode upper object.

After encoding and sending this object to the app, the __destruct() magic method is invoked and the file morale.txt is deleted.

