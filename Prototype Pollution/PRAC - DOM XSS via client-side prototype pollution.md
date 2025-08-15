Title: DOM XSS via client-side prototype pollution
Level: PRACTITIONER
Desc:  This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:
    Find a source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that allows you to execute arbitrary JavaScript.
    Combine these to call alert().
You can solve this lab manually in your browser, or use DOM Invader to help you. 

# Walkthrough:
I can try to add __proto__[foo]=bar to the URL and I can see this reflected in Object.prototype on Console:
<img width="1038" height="529" alt="image" src="https://github.com/user-attachments/assets/c2a48d16-6f78-4c93-b0e1-8f00346ea2a1" />

In searchLogger.js, notice that if the config object has a transport_url property, this is used to dynamically append a script to the DOM. Notice that no transport_url property is defined for the config object. This is a potential gadget for controlling the src of the <script> element.
<img width="741" height="328" alt="image" src="https://github.com/user-attachments/assets/a212f298-66f7-4873-8a13-ea6a6b09e46f" />

Using the prototype pollution source you identified earlier, try injecting an arbitrary transport_url property:
/?__proto__[transport_url]=foo

<img width="1025" height="564" alt="image" src="https://github.com/user-attachments/assets/5f6de871-fb4a-4d10-a50c-7fe9e25a57d5" />

Proper payload: `?__proto__[transport_url]=data:,alert(1);`

