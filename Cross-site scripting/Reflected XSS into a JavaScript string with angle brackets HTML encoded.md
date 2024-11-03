Title: Reflected XSS into a JavaScript string with angle brackets HTML encoded

After submiting the value in the search bar, it is added to the javascript code:
![image](https://github.com/user-attachments/assets/ea426b3f-a22d-48c7-a1c6-2e43d13bd5f5)

I can escape from ' in this javascript code and probably add my custom logic:

';alert(1)


![image](https://github.com/user-attachments/assets/8172b1ae-69c1-47e7-ac83-422a6c9b3bf9)
