# What is it
Access control is the application of constraints on who or what is authorized to perform action or access resources. In the context of web applications, access control is dependent on authentication and session management:
**Authentication**: confirms that the user is who they say they are.
**Session management**: identifies which subsequent HTTP requests are being made by that same user.
**Access control**: determines whether the user is allowed to carry out the action that they are attempting to perform.
Broken access controls are common and often present a critical security vulnerability. Design and management of access control is a complex and dynamic problem that applies business, organizational and legal constrains to a technical implementation. 
More of less it getting access to things that we shouldn't be able to get access to.


# How do we do it
The most basic example, is that we can change values in the *session storage* of the browser, if we are allowed to change the values in their, and we are getting different pages, then this is an example of broken access control.
Some broken access control situations, can also be seen in the wild, what if, when creating a user we see that we are getting assigned an ID?
- What should be the first thing to mangle then?
	- Check if we can access other users (their IDs)
What if we can see that, when creating a user, we get a request in [[Burp Suite]], that the server responds with a "isAdmin" flag?
- What happens if we set that to **true** in the request?
Broken Access control is just mainly about editing the request and response.
- Se if we can **break access patterns**


# Tools
- Burp Suite, with the Authorize plugin

# Mitigation
Don't handle the user role and user rights in a single role like "admin" or something.
- Handle it with permissions