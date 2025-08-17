Title: Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped
Level: PRACTITIONER
Desc: This lab contains a reflected cross-site scripting vulnerability in the search blog functionality. The reflection occurs inside a template string with angle brackets, single, and double quotes HTML encoded, and backticks escaped. To solve this lab, perform a cross-site scripting attack that calls the alert function inside the template string. 

# Walkthrough:

<img width="1237" height="531" alt="image" src="https://github.com/user-attachments/assets/ef6592d2-5a53-4ea7-800b-fef7e54037ca" />

In template literal we can try to run payload: `${alert(1)}`
<img width="1088" height="121" alt="image" src="https://github.com/user-attachments/assets/56f02d5d-b641-4381-ba80-3b08f2adbef9" />
