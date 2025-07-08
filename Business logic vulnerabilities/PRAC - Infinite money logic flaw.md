Title: Infinite money logic flaw
Level: Practitioner
Desc:  This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter 

Walkthrough:
I can sign in to newsletter and I can get code: PROMOR30
I also can buy gift card for 10$ and I can then use this gift card for my account to gain 10$.

However code PROMO30 works with purchasing gift card - so when I try to buy gift card for 10$ I can buy this card for 7$.
All I needed was to make loop with instructions as below:

![image](https://github.com/user-attachments/assets/28887d83-9ef9-4d2d-9333-a120a029e1ee)



```
Click Settings in the top toolbar. The Settings dialog opens.
Click Sessions. In the Session handling rules panel, click Add. The Session handling rule editor dialog opens.
In the dialog, go to the Scope tab. Under URL scope, select Include all URLs.
Go back to the Details tab. Under Rule actions, click Add > Run a macro. Under Select macro, click Add again to open the Macro Recorder.

Select the following sequence of requests:
POST /cart
POST /cart/coupon
POST /cart/checkout
GET /cart/order-confirmation?order-confirmed=true
POST /gift-card

Then, click OK. The Macro Editor opens.
In the list of requests, select GET /cart/order-confirmation?order-confirmed=true. Click Configure item. In the dialog that opens, click Add to create a custom parameter. Name the parameter gift-card and highlight the gift card code at the bottom of the response. Click OK twice to go back to the Macro Editor.
Select the POST /gift-card request and click Configure item again. In the Parameter handling section, use the drop-down menus to specify that the gift-card parameter should be derived from the prior response (response 4). Click OK.
In the Macro Editor, click Test macro. Look at the response to GET /cart/order-confirmation?order-confirmation=true and note the gift card code that was generated. Look at the POST /gift-card request. Make sure that the gift-card parameter matches and confirm that it received a 302 response. Keep clicking OK until you get back to the main Burp window.
Send the GET /my-account request to Burp Intruder. Make sure that Sniper attack is selected.
In the Payloads side panel, under Payload configuration, select the payload type Null payloads. Choose to generate 412 payloads.
Click on Resource pool to open the Resource pool side panel. Add the attack to a resource pool with the Maximum concurrent requests set to 1. Start the attack.
When the attack finishes, you will have enough store credit to buy the jacket and solve the lab. 
```
