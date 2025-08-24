Title: Server-side template injection with information disclosure via user-supplied objects
Level: PRACTITIONER
Desc:  This lab is vulnerable to server-side template injection due to the way an object is being passed into the template. This vulnerability can be exploited to access sensitive data.
To solve the lab, steal and submit the framework's secret key.
You can log in to your own account using the following credentials:
`content-manager:C0nt3ntM4n4g3r`

# Walkthrough:
We can edit product template.

Adding string: `${{<%[%'"}}%\` to product template and save.

<img width="1328" height="197" alt="image" src="https://github.com/user-attachments/assets/fd801b84-dc6f-4bc0-9033-cff24386d66a" />
After adding string to fuzz template injection I get an error indicating Django framework.

In django framework we have special template dedicated fot debugging: `{% debug %}`

We get this response after adding debugging string: 
<img width="1209" height="539" alt="image" src="https://github.com/user-attachments/assets/9f854702-dd69-486b-8cca-0dad5c069242" />

we have acces to the `django.conf.global_settings'` and we can ask (based on the documentation of course) for `{{settings.SECRET_KEY}}`

<img width="1027" height="426" alt="image" src="https://github.com/user-attachments/assets/336d62da-c09c-4be5-af96-851757bbbac2" />

