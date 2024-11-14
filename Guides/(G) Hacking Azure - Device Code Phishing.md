This is a write down/tutorial of how to use advance phishing to get access to on prem azure environment.
This is from the machine on PwnedLabs "Leverage Device Code Phishing for Initial Access".

## Entry Point:
We are required that we get a domain of the azure environment, this is easy since many times it's public available.
- If this isn't the case, we can use tools like [Oh356UserFinder](https://github.com/dievus/Oh365UserFinder), to verify the domain

## Scenario:
Our client _international Asset Management_ has asked us to perform a red team engagement. They want us to start externally as a threat actor would, try and breach their environment and access resources belonging to director or C-level executives. **Phishing is in scope**, and International Asset Management's IT partners have also agreed to be included in the test.