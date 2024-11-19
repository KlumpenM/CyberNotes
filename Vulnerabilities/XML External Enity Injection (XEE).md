# What is it


# How do we do it
Here is a **non-malicious** XML template that can be used for XEE injection:
```
<?xml vertion="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [
	<!ELEMENT foo ANY >
	<!Entity xee SYSTEM>
]>
```

# Tools


# Mitigation