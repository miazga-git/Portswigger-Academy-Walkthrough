Title: Single-endpoint race conditions
Level: PRACTITIONER
Desc:  This lab's email change feature contains a race condition that enables you to associate an arbitrary email address with your account.

Someone with the address carlos@ginandjuice.shop has a pending invite to be an administrator for the site, but they have not yet created an account. Therefore, any user who successfully claims this address will automatically inherit admin privileges.

To solve the lab:

    Identify a race condition that lets you claim an arbitrary email address.
    Change your email address to carlos@ginandjuice.shop.
    Access the admin panel.
    Delete the user carlos

You can log in to your own account with the following credentials: wiener:peter.

You also have access to an email client, where you can view all emails sent to @exploit-<YOUR-EXPLOIT-SERVER-ID>.exploit-server.net addresses. 

# Walkthrough
