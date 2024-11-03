Ttile: DOM XSS in document.write sink using source location.search

I can type anything in the search bar, and it's reflected on the page. It is also visible in the URL as an parameter.
![image](https://github.com/user-attachments/assets/a805afa0-eefe-4610-9202-078facddc1a0)

I am checking out the source code, and I can see the following code:
![image](https://github.com/user-attachments/assets/4c7e6178-2234-4059-9da3-2c7ac867dd3e)

We have line document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');
It takes value of the URL parameter and under query builds IMG objects with it. It also uses document.write() function to inject objects into website. 
So I can escape from this and maybe add yet another object into document.write() function. Let's try:

payload would be like this: 
'"> - this part to escape string and img tag. 
Now we can add another element, let's use: <svg onload=alert(1)>

complete payload is: '"><svg onload=alert(1)>

Let's try injection:
![image](https://github.com/user-attachments/assets/c0516e10-4268-423c-83fb-fcd1f668f4e9)

It is working!
![image](https://github.com/user-attachments/assets/3bbfc7ce-e92b-477b-9605-708f676a0bf0)
