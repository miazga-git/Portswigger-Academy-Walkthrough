Title: Web cache poisoning via ambiguous requests
Level: Practitioner
Desc: This lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end application handle ambiguous requests. An unsuspecting user regularly visits the site's home page.
To solve the lab, poison the cache so the home page executes alert(document.cookie) in the victim's browser. 

# Walkthrough:
<img width="1354" height="664" alt="image" src="https://github.com/user-attachments/assets/ae579626-5b98-4d22-b430-71b253fb4ed4" />
After adding additional, second Host header I can get response from the app, what is more interesting, I can see my value of second host being reflected in the response.


Remove the second Host header and send the request again using the same cache buster. Notice that you still receive the same cached response containing your injected value.
<img width="1225" height="486" alt="image" src="https://github.com/user-attachments/assets/a99478f6-a8d6-4424-847f-2886e6aec565" />

<img width="1191" height="470" alt="image" src="https://github.com/user-attachments/assets/c74baaf0-6477-46c0-8e48-8a2dc19802b4" />

I placed malicious code on the exploit server and then I injected the link to the server resource into the cache of a site:
<img width="954" height="624" alt="image" src="https://github.com/user-attachments/assets/984500bf-5e98-456f-bbfa-eb8d62da81a3" />


<img width="1261" height="318" alt="image" src="https://github.com/user-attachments/assets/da82f505-baf0-4037-a249-10ca72646518" />

<img width="1379" height="625" alt="image" src="https://github.com/user-attachments/assets/b65d180b-deae-45e6-959a-d2d1c98444c6" />
