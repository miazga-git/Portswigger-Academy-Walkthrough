Title: DOM XSS in jQuery anchor href attribute sink using location.search source

That's the submit feedback page:
![image](https://github.com/user-attachments/assets/d5defb84-48cc-4ebe-bf4b-4fcc5a0e2822)

First of all, let's check out the source code:
![image](https://github.com/user-attachments/assets/b6b15737-3aea-4314-b809-8f69f036a12b)

So, using the value of the parameter in URL the HREF of return button is being set. So, I guess that we can inject something into the URL parameter, let's try with this:

```javascript:alert('XSS')```

URL with malicious parameter:
![image](https://github.com/user-attachments/assets/313283e5-8b32-4652-8c3c-c7773a6c9f3a)

After clicking back we have XSS!

![image](https://github.com/user-attachments/assets/9234c594-4abf-438b-87c7-fbae9b3eed0b)



