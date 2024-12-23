# Overview of top commands
You can see what commands that you use the most in Linux with the command:
- This is for the top 10, you can change the last argument
```bash
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
```