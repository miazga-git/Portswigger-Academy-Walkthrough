Title: Reflected DOM XSS
Level: Practitioner
Desc:  This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. A script on the page then processes the reflected data in an unsafe way, ultimately writing it to a dangerous sink.

To solve this lab, create an injection that calls the alert() function. 

When I searching by keyword, I got response like that:
![image](https://github.com/user-attachments/assets/99c1edad-0921-4e9c-ae7e-20926de6871e)

The second one is interesting: 
![image](https://github.com/user-attachments/assets/ce4a4fa3-8d3e-4dba-8e57-a930bca7d66b)
It is GET request to the path: search-results and in response it contains "searchTerm":"test" - test is the variable that we control

Let's see how the source code of the page looks like: 
![image](https://github.com/user-attachments/assets/2fd53c8e-0e64-4c03-bb5a-7642f86c4367)

![image](https://github.com/user-attachments/assets/e482f2d7-cdab-4246-b257-80b96a8ee3a8)

Some interesting facts:
- eval() function in use
- search() function uses search-results as parameter

So, the workflow is: I submit word as search keyword, i background we have request to search-results, which returns data in JSON, and some parts of that JSON we can control, then this response is used first by search function, and then in eval function. We need to escape JSON to make our javascript executable.

I try payload: `test"};alert(1)` however it is escaped by application:
![image](https://github.com/user-attachments/assets/74c75d64-4ca6-419a-ac52-ecca11d6432d)

So I try to escape escaping: `test\"};alert(1)`

After many attempts, I see that payload need to be like that: `\"-alert(1)}//`

Things to note:
- payload with sign ; didn't work, it should be - sign
- the alert function still need to be in the json, not after closing json
- there is always a good idea to comment rest by //

![image](https://github.com/user-attachments/assets/487a06de-43e3-429f-8a32-9c20f076e9be)
