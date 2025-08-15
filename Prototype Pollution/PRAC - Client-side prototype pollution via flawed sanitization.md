Title: Client-side prototype pollution via flawed sanitization
Level: PRACTITIONER
Desc:  This lab is vulnerable to DOM XSS via client-side prototype pollution. Although the developers have implemented measures to prevent prototype pollution, these can be easily bypassed.
To solve the lab:
    Find a source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that allows you to execute arbitrary JavaScript.
    Combine these to call alert().

# Walkthrough:

Not working:
```
?constructor.prototype.foo=bar
?__proto__.foo=bar
?__proto__[foo]=bar
```

Go to the Sources tab and study the JavaScript files that are loaded by the target site. Notice that deparamSanitized.js uses the sanitizeKey() function defined in searchLoggerFiltered.js to strip potentially dangerous property keys based on a blocklist. However, it does not apply this filter recursively. 
<img width="609" height="166" alt="image" src="https://github.com/user-attachments/assets/fecb2ea1-a327-44fb-bd3b-c2a948507df3" />

We can do some trick: we can use for example : `?__pro__proto__to__[foo]=bar`
<img width="984" height="510" alt="image" src="https://github.com/user-attachments/assets/f54d5f94-3319-4834-a8c2-7d13435c5839" />

Study the JavaScript files again and notice that searchLogger.js dynamically appends a script to the DOM using the config object's transport_url property if present.
Notice that no transport_url property is set for the config object. This is a potential gadget.

<img width="796" height="210" alt="image" src="https://github.com/user-attachments/assets/9d98f8da-f2c2-4b75-b903-1474c5a1a0cf" />

<img width="1034" height="601" alt="image" src="https://github.com/user-attachments/assets/d7f5ff4f-ddd0-4204-bb7d-e19a4a58cf9e" />

`https://0a2d003e0423e109804bdfb20078000d.web-security-academy.net/?__pro__proto__to__[transport_url]=data:,alert(1)`


