Title: Basic server-side template injection (code context)
Level: Practitioner
Desc:
This lab is vulnerable to server-side template injection due to the way it unsafely uses a Tornado template. To solve the lab, review the Tornado documentation to discover how to execute arbitrary code, then delete the morale.txt file from Carloss home directory. 
You can log in to your own account using the following credentials: wiener:peter 

Walkthrough:
In user settings I can see new option - Preferred Name option. I can make request to choose either my nickname or first name to be displayed.
![image](https://github.com/user-attachments/assets/663069f7-a39c-4414-ac09-ced836467f87)

I can at the end of the paramter try to paste SSTI injection: `{{8*8}}` . # It is template for Tornado template.
After that I need to go to the comment setion of choosen post where I recently added a comment and I can see an error:

![image](https://github.com/user-attachments/assets/b5bf350d-ba6a-4464-97e5-24c7095149e0)

What is interesting about this error - it is a clue, we can see only part of our payload. We see only `{{8*8`, but we provided `{{8*8}}`.
Based on that I can assume, that user.first_name is between `{{` and `}}`, so after adding to strin my payload we can have something like that : `{{ user.first_name {{8*8}} }}` and it reduces to the `{{ user.first_name {{8*8}}` and curly brackes make an effect so we end with : `user.first_name {{8*8`.
We now know, we need to close curly brackets before adding our own code to execute on the template rules. So we neeed to provide payload: `}}{{8*8`.

![image](https://github.com/user-attachments/assets/4ebe5033-23b7-4bb1-9e62-1f24f5c89a1b)


![image](https://github.com/user-attachments/assets/7a8b14ce-c8de-4f8d-a861-368b91604901)

To execute linux commands in Tornado template we need to use payload: `blog-post-author-display=user.first_name}}{{__import__('os').system('ls')`

And next I use payload to delete file: `blog-post-author-display=user.first_name}}{{__import__('os').system('rm -f morale.txt')`

We did it!
