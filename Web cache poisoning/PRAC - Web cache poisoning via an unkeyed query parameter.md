Title: Web cache poisoning via an unkeyed query parameter
Level: Practitioner
Desc:  This lab is vulnerable to web cache poisoning because it excludes a certain parameter from the cache key. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the cache with a response that executes alert(1) in the victim's browser. 
Hint: Websites often exclude certain UTM analytics parameters from the cache key. 

# Walkthrough:
"UTM parameters like utm_content are good candidates to check during testing."

<img width="1576" height="545" alt="image" src="https://github.com/user-attachments/assets/125397f8-06b3-4ae2-a76f-92bc2c334b32" />

Below request I use to poison cache for all: 
<img width="1552" height="422" alt="image" src="https://github.com/user-attachments/assets/d05a44e7-6001-4a26-8782-ea7e35c8ad7e" />


<img width="1380" height="381" alt="image" src="https://github.com/user-attachments/assets/108e359d-39fd-4537-afa7-a3f7fda23589" />

But how to guess, that we need to use utm_content parameter.
"Use Param Miner's "Guess GET parameters" feature to identify that the parameter utm_content is supported by the application. "

Let's try param miner then:
<img width="885" height="320" alt="image" src="https://github.com/user-attachments/assets/992c38e2-d6bd-45fc-903f-427093cc779c" />


