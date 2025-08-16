Title: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped
Level: PRACTITIONER
Desc:  This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped.
To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function. 

# Walkthrough:
<img width="1236" height="176" alt="image" src="https://github.com/user-attachments/assets/31d66cca-32ea-4345-b587-9ea04b8596b2" />

Try sending the payload test\payload and observe that your backslash doesn't get escaped. 

`\'-alert(1)//`

`//` - that's the comment in javascript, not the `#` sign, we are not in sql.
