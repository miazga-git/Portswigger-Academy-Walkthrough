Title: Low-level logic flaw
Level: Practitioner
Desc:  This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter 

# Walkthrough:

So I try to add 3 digit quantity of leather jacket and I get an error. It gives me idea to test if we can do kind of "buffer overflow/integer overflow".
![image](https://github.com/user-attachments/assets/0ad1bc34-6f8d-4dd6-8008-b2a3448e63e2)

So I go to the intruder and I try to send many requests with adding 99 leather jackets.

![image](https://github.com/user-attachments/assets/548c6a95-bffc-457b-a723-5244c2b10b51)

![image](https://github.com/user-attachments/assets/0c739be5-c9f1-4267-9b16-eb8da71b9fb1)


After this attack in my basket I can see, that my total price increase and suddely it becomes negative and then it goes towards 0. So I need to add proper number of jackets to be between 0 and 100$.

![image](https://github.com/user-attachments/assets/f20d3ced-d72e-4124-b59d-6908ee4edb9e)

![image](https://github.com/user-attachments/assets/825e9880-4aac-40a0-841c-1aba27fefa02)

![image](https://github.com/user-attachments/assets/8ab62c6d-32af-4302-bf1e-3d2818140c3e)

![image](https://github.com/user-attachments/assets/c6a47d37-e22b-4f57-a6fe-0104555607d6)

We did it!
