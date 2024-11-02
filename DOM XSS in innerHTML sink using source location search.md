Title: DOM XSS in innerHTML sink using source location.search

We alread know the application so let's jump into the source code. We can see interesting fuction here:



![image](https://github.com/user-attachments/assets/61e2d6f1-033f-4f44-8aac-8ba74ef3ca7f)

According to the code, we can inject html tags using .innerHTML. Let's see how it is working using simple tags <b>test</b>

After inspecting reflected on the site element we can see something like that:
![image](https://github.com/user-attachments/assets/b4f3a591-2213-4cf5-b8f7-2f2897e8261e)

So, probably there we can inject everything, including malicious content. 
I tried payload like that:
<img src=x onerror=alert('XSS Attack!')>

But this didn't work for me. To be honest, I check out the solution and I found that I need to replace string in alert() function to number:

<img src=1 onerror=alert(1)>

Here we go!
![image](https://github.com/user-attachments/assets/c779784c-88ee-4559-9d6f-a7dab9171f9c)

And after inspecting it:
![image](https://github.com/user-attachments/assets/21ee4237-cb33-4cb4-9ed6-8c84c422d177)
