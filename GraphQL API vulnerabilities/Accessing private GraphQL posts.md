Title: Accessing private GraphQL posts
Desc: The blog page for this lab contains a hidden blog post that has a secret password. To solve the lab, find the hidden blog post and enter the password. 

![image](https://github.com/user-attachments/assets/0b167cf7-846f-4d21-88f0-67cba8f15f64)


I changed method from GET to POST and added Content-Type: application/json

I also changed the path to `/graphql/v1`. 

I get response "Body cannot be empty"

![image](https://github.com/user-attachments/assets/0d7de297-6d15-43a1-8aee-ee4f0b092b00)

![image](https://github.com/user-attachments/assets/708ff367-d16b-422d-9b8b-fa3a17303fd6)

hint: `In Repeater, right-click anywhere in the Request panel of the message editor and select GraphQL > Set introspection query to insert an introspection query into the request body. `

----------That part was not working for me because I got invalid json in response to my instrospection query-------------------
I should use tool: http://nathanrandal.com/graphql-visualizer/ and the introspection query and I get structure:
-----------------------------



![image](https://github.com/user-attachments/assets/0d76580f-5a8d-4dda-a868-1f96fa2c2c0e)

`{"query": "{getBlogPost(id: 3) {id name listed}}"}`
![image](https://github.com/user-attachments/assets/174610c7-cedf-4414-a850-801219b91cc9)


`{"query": "{getBlogPost(id: 3) {id image title author date summary paragraphs isPrivate postPassword}}"}`

![image](https://github.com/user-attachments/assets/03f17fbb-81c8-4c07-9713-01a214545b2f)





