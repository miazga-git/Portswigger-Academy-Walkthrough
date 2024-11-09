Title: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded
Level: Practitioner
Desc: This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within the search functionality.

AngularJS is a popular JavaScript library, which scans the contents of HTML nodes containing the ng-app attribute (also known as an AngularJS directive). When a directive is added to the HTML code, you can execute JavaScript expressions within double curly braces. This technique is useful when angle brackets are being encoded.

To solve this lab, perform a cross-site scripting attack that executes an AngularJS expression and calls the alert function. 

From the solution: "View the page source and observe that your random string is enclosed in an ng-app directive."
![image](https://github.com/user-attachments/assets/b194137c-2561-44dd-9fb0-2deed7442315)


payload: `{{constructor.constructor('alert(1)')()}}`

