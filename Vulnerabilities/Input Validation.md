# What is it
Input validation is performed to ensure only properly formed data is entering the workflow in an information system, preventing malformed data from persisting in the database and triggering malfunction of various downstream componetns.
Input validation should happen as early as possible in the data flow, preferable as soon as the data is received from the external party.
Input validation should not be used and the *primary* method of prevention [[Cross-site Scripting (XSS)]], [[SQL Injection]] and other attacks.