3 Linux User Setup with Non-Interactive Shell

- In production environments, many Linux users are created only for running applications or services, not for human access.

- To improve security, we assign a non-interactive shell like `/sbin/nologin` or `/bin/false`. This prevents SSH or terminal login while still allowing the account to own files and run processes.

- This follows the Principle of Least Privilege and reduces attack surface. For example, if a web application service account gets compromised, the attacker cannot obtain an interactive shell session on the server.


Interview Explanation :
A non-interactive Linux user is a secure service account used to run applications or automation without allowing direct shell login, helping enforce least privilege and reduce server attack surface in production environments.