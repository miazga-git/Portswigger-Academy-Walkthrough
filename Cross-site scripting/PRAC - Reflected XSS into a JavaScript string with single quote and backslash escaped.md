Title: Reflected XSS into a JavaScript string with single quote and backslash escaped
Level: PRACTITIONER
Desc:  This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped.
To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function. 


# Walkthrough:
I tried to search by `miazga'` but it was escaped.
<img width="1214" height="150" alt="image" src="https://github.com/user-attachments/assets/b2d39e53-1dee-46b5-adc1-941b579e5531" />
`<script>alert(1)</script>` - it gives some effect to me
<img width="1108" height="203" alt="image" src="https://github.com/user-attachments/assets/5eb0a905-34a6-41c6-ab82-550720a6a887" />

`</script><script>alert(1)</script>` - that's valid payload.



