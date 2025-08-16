Title: Reflected XSS with some SVG markup allowed
Level: PRACTITIONER
Desc: This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.
To solve the lab, perform a cross-site scripting attack that calls the alert() function. 

# Walkthrough:

<img width="1405" height="226" alt="image" src="https://github.com/user-attachments/assets/57559dd6-bd4d-4eab-9eb5-e7b639b32ff1" />

copy all tags to clipboard from this site: https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

I make intruder attack to try all tags possible.

After intruder attack I can see, that couple elements are possible to use on the web page: 
`<animatetransform>`
`<image>`
`<svg>`

Now we can creaft combo: `<svg><animatetransform%20=1>`

And now again intruder but this time we need to make attack here: 
`<svg><animatetransform%20§§=1>`

from site copy all events and run an attack: `https://portswigger.net/web-security/cross-site-scripting/cheat-sheet`

<img width="1313" height="406" alt="image" src="https://github.com/user-attachments/assets/ac6898f0-cd01-497c-94ee-ea362b5f9825" />

`onbegin` that's the one!

our malicious link: `https://0a9d00dc03ebe2a5806403e400d4006a.h1-web-security-academy.net/?search=%3Csvg%3E%3Canimatetransform%20onbegin=alert(1)%3E`





