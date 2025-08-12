Title: Finding a hidden GraphQL endpoint
Level: PRACTITIONER
Desc:  The user management functions for this lab are powered by a hidden GraphQL endpoint. You won't be able to find this endpoint by simply clicking pages in the site. The endpoint also has some defenses against introspection.
To solve the lab, find the hidden endpoint and delete carlos.
Learn more about Working with GraphQL in Burp Suite. 

# Walkthrough:
<img width="1233" height="444" alt="image" src="https://github.com/user-attachments/assets/a3b51860-e8ad-4345-acd9-781bb0127995" />
under /api we have graphql.

POST method not allowed for /api endpoint:
<img width="1239" height="507" alt="image" src="https://github.com/user-attachments/assets/c10cae0d-4e96-4861-a5e0-53b400e4ac88" />

we did it by: `GET /api?query=query%7B__schema%0A%7BqueryType%7Bname%7D%7D%7D`
<img width="1263" height="515" alt="image" src="https://github.com/user-attachments/assets/39ec4eed-c0ef-4727-8282-c518d029932d" />

<img width="1301" height="422" alt="image" src="https://github.com/user-attachments/assets/b41967fd-6be7-4227-8d9b-41071f624cc1" />
Introspection query is not possible.

However after adding `%0a` - newline character before __schema we have full response:
<img width="1214" height="501" alt="image" src="https://github.com/user-attachments/assets/5a38e60a-9932-4d90-b398-3ddf97b1bdf0" />

I use site http://nathanrandal.com/graphql-visualizer/ to read the response.
<img width="1817" height="633" alt="image" src="https://github.com/user-attachments/assets/3dddbef8-7527-4f12-8454-54f388002665" />

Freakin helpfull option:
<img width="1359" height="453" alt="image" src="https://github.com/user-attachments/assets/95cc8e7c-55a7-4fa9-aa6c-f76f6d3c48f7" />

In Target I found request to delete user
<img width="1233" height="601" alt="image" src="https://github.com/user-attachments/assets/5431ddef-3339-465b-9f35-f04fe88ae894" />

We have also endpoint to search through users:
<img width="1272" height="379" alt="image" src="https://github.com/user-attachments/assets/1e02e179-caf2-43c5-b0c4-935b8355874d" />





