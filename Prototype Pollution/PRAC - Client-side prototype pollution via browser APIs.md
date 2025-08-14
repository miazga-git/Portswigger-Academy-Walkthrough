Title: Client-side prototype pollution via browser APIs
Level: PRACTITIONER
Desc:  This lab is vulnerable to DOM XSS via client-side prototype pollution. The website's developers have noticed a potential gadget and attempted to patch it. However, you can bypass the measures they've taken.
To solve the lab:
    Find a source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget property that allows you to execute arbitrary JavaScript.
    Combine these to call alert().
You can solve this lab manually in your browser, or use DOM Invader to help you. 

# Walkthrough: 
## Finding prototype pollution source:
1) In your browser, try polluting Object.prototype by using below in URL:
`/?__proto__[foo]=bar`

2) Open DevTools panel, go to the Console and enter: `Object.prototype`

3) Look for properties and you can see, that you polluted Object.prototype with foo = bar.

## Indentify a gadget
1) In DevTools go to the Sources tab.
2) Study the JavaScript files that are loaded by the target site and look for any DOM XSS sinks.
3) In `searchLoggerConfigurable.js`, notice that if the `config object` has a `transport_url` property, this is `used to dynamically append a script to the DOM`.
4) Observe that a `transport_url property is defined for the config object, so this doesn't appear to be vulnerable`.
5) Observe that the next line uses the `Object.defineProperty()` method `to make the transport_url unwritable and unconfigurable`. However, notice that `it doesn't define a value property`.

## Craft an exploit 
1) Using the prototype pollution source you identified earlier, try injecting an arbitrary value property:
    `/?__proto__[value]=foo`
2) In the browser DevTools panel, go to the Elements tab and study the HTML content of the page. Observe that a <script> element has been rendered on the page, with the src attribute foo.
<img width="1011" height="625" alt="image" src="https://github.com/user-attachments/assets/6f9c7d74-ae92-487d-877b-23fe508c14ec" />
3) Change that to: `/?__proto__[value]=data:,alert(1);`

# AUTO - Walkthrough: 
Enable dom invader option:
<img width="1688" height="435" alt="image" src="https://github.com/user-attachments/assets/097a9ed4-60e8-425c-bf05-4db1fdc968ac" />

Open DevTools and one of the windows is invader tab:
<img width="1419" height="382" alt="image" src="https://github.com/user-attachments/assets/7c929d25-346f-4f84-8e9a-5e973486742f" />
Enable prototype pollution attack in dom invader:
<img width="513" height="403" alt="image" src="https://github.com/user-attachments/assets/a7274f31-b7ec-4583-9b51-a9fa0c628903" />

DOM INVADER HAVE FOUND 2 SOURCES:
<img width="1867" height="527" alt="image" src="https://github.com/user-attachments/assets/c27f1aa1-6bea-4445-9e4a-c9085e54eae0" />

Clicking "scan for gadgets".
A new tab opens in which DOM Invader begins scanning for gadgets using the selected source. 

When the scan is complete, open the DevTools panel in the same tab as the scan, then go to the DOM Invader tab.

Observe that DOM Invader has successfully accessed the script.src sink via the value gadget.

Click Exploit. DOM Invader automatically generates a proof-of-concept exploit and calls alert(1).

