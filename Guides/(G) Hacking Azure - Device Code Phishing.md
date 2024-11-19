This is a write down/tutorial of how to use advance phishing to get access to on prem azure environment.
This is from the machine on PwnedLabs "Leverage Device Code Phishing for Initial Access".

# Entry Point:
We are required that we get a domain of the azure environment, this is easy since many times it's public available.
- If this isn't the case, we can use tools like [Oh356UserFinder](https://github.com/dievus/Oh365UserFinder), to verify the domain

# Scenario:
Our client _international Asset Management_ has asked us to perform a red team engagement. They want us to start externally as a threat actor would, try and breach their environment and access resources belonging to director or C-level executives. **Phishing is in scope**, and International Asset Management's IT partners have also agreed to be included in the test.

# What to do first?
## Scanning
First just go to the site, and look around see if we can find information.
Start by the first step: [[Scanning and Enumeration]], and here is the guide for [[(G) Scanning]]. Since we are working against a Azure Environment, it's good to get domain info or some information about their Email structure, that's bound to their domain.

## Enumeration
When we find an email, that we might be certain that's from the client we are pen testing, we can do some initial enumeration against the domain.
One good thing to do, is to figure out how they are running things, where is their mail server located. What services are they using?
To answer this question, we can look at DNS records, and one good way of doing this in Linux is using the **dig** command:
```
dig <domain> amy +noall +answer
```
This gives us all the fields, that dig is going to pull from the domain.
If the above command, doesn't give us a mail server or hint to where the mail server is, we can just run:
```
dig <domain>
```
This gives us all the information from dig, but this is just not sorted or pretty printed.
If this still doesn't give you the information about the mail server, we can do some deeper enumeration to get the information.
We can use a website, to see if the clients domain is using Azure and if its managed or federated. But what does this two things mean?
**Managed**:
This means that it's **cloud only**, it means that it uses Entra ID identity management.
**Federated**:
This means that it might use an ADFS (Active Directory Federated Services) which is an external IdP (Identity Provider).
We can use the website login.microsoftonline.com/getuserrealm.srf?login=domain&xml=1, where "domain" is the domain of the client that we are testing against.
If we get something on the screen, a output could look like this:
![[Pasted image 20241119170405.png]]
This means that the client is using Azure/Outlook, and we can see that it's **managed**.
Now that we know the client, is using a managed Azure instance, but just to make sure, we can also check the IP address of the domain.
To start with, we need to make sure that the client's website is online:
```
ping <domain>
```
This is just to get the IP address of the domain.
We can get more information and confirmation about the domain being in Azures IP space, we can do this with the command:
```
curl https://ipinfo.io/<ip address>
```
If we get information that states the IP address belonging to Azure or Microsoft, we would normally see it as: `org: <somthing> Microsoft Corporation`.
*This is just further confirming the information that we already have*.

Now all this have confirmed, that **if** we got a valid email, as the first part of the enumeration that we did against the target, we have valid email address.
Now we can start to think about what we should do to gain access to the target:
- Should we look for breached credentials
- Can we just try to brute-force it.
- Is phishing in scope? If it is, this might be the go to.
One quick things that we can check, with the valid email(s) of the domain is that we can check the website: https://dehashed.com/ to see if their domain or email addresses where is a past leak. But there is a section on [[Dehashed]].
Here we can get the following: (If it was a part of a breah)
- Username
- Plain text Password
- Hashed Password (We can try to crack it)
Then we can just spray the login form, to see if any of them works.
**But this is not the section for this*

# Device Code Phishing
Since this is the guide focusing on Device Code Phishing, we will try to do an attempt, based on this [article](https://aadinternals.com/post/phishing/). This is a step by step guide, on how Device Code Phishing.
## Quick Summary
When you authenticate to Azure, you can choose the options of doing "Device Code", and when we do this it brings us to a page that asks you to enter in a code.

*If you want to try  this yourself, do the following command*:
```
az login --use-device-code
```
*This should prompt a window, where you can type in a generated code to authenticate, this is just for understanding how it works.*
This is what the victim would see, if you sent them the link.

## Phishing
Now that we have learned what it is, we want to do the actual phishing part, meaning that we want to send an email, and we want to send it urgently. What tool is good for this specific task?
**ChatGPT** (or if you have access to it **FraudGPT**)
We can say something like this:
```
Hello robot friend,

Please write an email that explains to the user they need to go to a URL and enter a specific code to confirm their Microsoft account. Make it urgent, because if they don't do this their account will expire and they will get in trouble with their supervisor

Make it sound porfessionsal, I am sending this from the IT Helpdesk for my org.
```

When we have our specially crafted email, we can get to work on our phishing campaign. To do this, we type in the command, so that we can get a link that they need to sign into:
```
az login --use-device-code
```
This generates the link: `https://microsoft.com/devicelogin` and a code `sequence of letters`.
This URL and code looks genuine, meaning that they are more likely to fall into our trap.

# Something that we require:
For this to work, we need to do the following:
- Send the mail, from a domain that's close to the original, if it's `.com`, we can purchase `.cam`. Since the mind will autocorrect it (because the first and last letter is the same)
- We can use different kind of "a", if the domain we are trying to phish has an "a" in the name.
- Host the VM on the cloud, so that the terminal hosting the phishing link, doesn't go down.

# If successful
If we are in the great case where the victim types in **our** predefined code, because it's a legit website and maybe legit email.
Then we are getting something along the lines of:
![[Pasted image 20241119174217.png]]

Now we are authenticated in the terminal, we can various types of stuff:
```
az account show
```
This shows the information of the user (but unfortunately not the password)

But from there, we can enumerate different recourses inside the domain, since we are authenticated.