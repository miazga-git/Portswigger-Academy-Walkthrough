Title: Multi-endpoint race conditions
Level: Practitioner
Desc:  This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.
To solve the lab, successfully purchase a Lightweight L33t Leather Jacket.
You can log into your account with the following credentials: wiener:peter. 


# Walkthrough

## Exploring warming up the connection

```
Send both the POST /cart and POST /cart/checkout request to Burp Repeater.

In Repeater, add the two tabs to a new group. For details on how to do this, see Creating a new tab group

Send the two requests in sequence over a single connection a few times. Notice from the response times that the first request consistently takes significantly longer than the second one. For details on how to do this, see Sending requests in sequence.

Add a GET request for the homepage to the start of your tab group.

Send all three requests in sequence over a single connection. Observe that the first request still takes longer, but by "warming" the connection in this way, the second and third requests are now completed within a much smaller window.

Deduce that this delay is caused by the back-end network architecture rather than the respective processing time of the each endpoint. Therefore, it is not likely to interfere with your attack.
```


## Walkthrough
1. Add gift card to basket so when comes to validating basket during /cart/checkout request it says, that it is OK
2. Next add request POST /cart/checkout to repeater (this request makes transaction)
3. Next add request POST /cart, but it should be before /cart/checkout request and productId of this request should be 1 (jacket id)
4. In my case it was helpful to also add warmingup request to / before those two requests.
5. Sending group (parallel)

![image](https://github.com/user-attachments/assets/3c474344-6778-4a2d-9609-c326949ecce0)

![image](https://github.com/user-attachments/assets/7cb45f25-10aa-4d9e-b991-6453c1f91c55)

![image](https://github.com/user-attachments/assets/223f01d8-9ce1-4412-bc33-f24f0e1f5595)

