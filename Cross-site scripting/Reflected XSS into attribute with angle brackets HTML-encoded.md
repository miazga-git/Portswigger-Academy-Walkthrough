Title: Reflected XSS into attribute with angle brackets HTML-encoded


Attack using XSS list in BurpSuite intruder:
![image](https://github.com/user-attachments/assets/4785b44d-b818-4ef1-9bcb-e19a7a00edb6)

payload: "autofocus/onfocus=alert(1)//'


it also works: "onmouseover="alert(1)

It is because we inject code into search bar, our search word is reflected in the search bar also.
![image](https://github.com/user-attachments/assets/bb427e75-19ae-4bad-9150-5e80a611a337)
