Title: DOM-based open redirection
Level: PRACTITIONER
Desc: This lab contains a DOM-based open-redirection vulnerability. To solve this lab, exploit this vulnerability and redirect the victim to the exploit server. 

# Walkthrough:
I have found vulnerable code on the site: 
<img width="1378" height="161" alt="image" src="https://github.com/user-attachments/assets/5254ddd8-53bb-4927-b3b6-9fa8e89b7587" />
It is on this url for example: `https://0aef00b1046cad3d82606fb700ee00c4.web-security-academy.net/post?postId=1`

```
                    <div class="is-linkback">
                        <a href='#' onclick='returnUrl = /url=(https?:\/\/.+)/.exec(location); location.href = returnUrl ? returnUrl[1] : "/"'>Back to Blog</a>
                    </div>
```
Upper function in onclick is crucial - it tells, that if we are on url like: https://webpage.com/url=https://another-webpage.com it will take from that url only part from url paramter and it will return to that.
So we can try to refer to url like: `https://0aef00b1046cad3d82606fb700ee00c4.web-security-academy.net/post?postId=1#/url=https://test` and it takes us to `https://test` after clicking button "Back to Blog".

<img width="1502" height="95" alt="image" src="https://github.com/user-attachments/assets/2b8cdefa-0b13-4d0a-b52f-0e88bccaf6e7" />

So now our payload, which we can send to the victim is:
`https://0aef00b1046cad3d82606fb700ee00c4.web-security-academy.net/post?postId=1#/url=https://exploit-0abf00a20497ad5682a46eca018e00e5.exploit-server.net/exploit`

So that is a proper answer, but the lab only accepts:
`https://0aef00b1046cad3d82606fb700ee00c4.web-security-academy.net/post?postId=1&url=https://exploit-0abf00a20497ad5682a46eca018e00e5.exploit-server.net/exploit`
