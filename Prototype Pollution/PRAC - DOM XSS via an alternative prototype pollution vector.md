Title: DOM XSS via an alternative prototype pollution vector
Level: PRACTITIONER
Desc:  This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:
    Find a source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that allows you to execute arbitrary JavaScript.
    Combine these to call alert().
You can solve this lab manually in your browser, or use DOM Invader to help you. 

Hint: Pay attention to the XSS context. You need to adjust your payload slightly to ensure that the JavaScript syntax remains valid following your injection. 

# Walkthrough:
This time pollution Object.prototype via `/?__proto__[foo]=bar` is not working.
Let's try alternative: `/?__proto__.foo=bar`

<img width="1113" height="514" alt="image" src="https://github.com/user-attachments/assets/b79af103-b9d4-4f6c-90a3-5dded1f44bca" />
This time it was successful.

Finding the gadget.
```
Notice that there is an eval() sink in searchLoggerAlternative.js.
Notice that the manager.sequence property is passed to eval(), but this isn't defined by default.
```

Try to make payload: `/?__proto__.sequence=alert(1)`
<img width="785" height="152" alt="image" src="https://github.com/user-attachments/assets/d302d77f-2e0d-4c6c-ac9b-f017aae21e93" />
I made an error.

We needed to add `/?__proto__.sequence=alert(1)-` 

Look at the code: 
<img width="828" height="320" alt="image" src="https://github.com/user-attachments/assets/4f5d09fd-8acc-4da0-b371-b334ec4acb6c" />
