Ttile: Stored DOM XSS
Level Practitioner
Desc: This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the alert() function. 

![image](https://github.com/user-attachments/assets/f32e1063-7556-4631-9e15-b9ba23adfc57)
![image](https://github.com/user-attachments/assets/2fec70d5-5113-4cc4-a01f-5b0af4cd7d23)


So, the XSS we can find in comment field, before rendering our comment, javascript use function to escape special characters like <,>.
Below you can see the function:
html.replace('<', '&lt;').replace('>', '&gt;')

What is interesting, it only executes once, firstly for sign `<` and secoundly for sign `>`
So any payloads like that would work:
`<><img src=1 onerror=alert(1)>`
`<img src=1 onerror=alert(1)><img src=1 onerror=alert(1)>`
