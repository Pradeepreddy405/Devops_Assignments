### 1.Custom Apache User Setup

- This is a Linux system administration and DevOps security task.
- You are creating a dedicated Linux user account for a web application running on Apache.

## Why this task ?
In real companies, multiple applications run on the same server. Let say below applications runs on same server without isolation
 - 1 Finance app
 - 2 HR app
 - 3 Ecommerce app
 - 4 Internal dashboard
 - If all the users run under the same user called "/var/www-data"	
		
```
	/var/www/
	├── finance-app
	├── hr-app
	├── ecommerce-app
```
- Problmes:	
 - 1 one hacked app can access another app
 - 2 permissions become messy
 - 3 auditing becomes difficult
 - 4 security isolation becomes weak
 
 - To avoid this problems , companies uses one user for one application , By doing this we can achieve
	1 user isolation
	2 process isolation
	3 least privilege security

---
BEFORE

                    SERVER
------------------------------------------------
 Apache Service (www-data)

    ├── HR Application
    ├── Ecommerce Application
    ├── Payroll Application
    └── Inventory Application


If Ecommerce app gets hacked:
	- attacker can access HR files
	- attacker can modify payroll app
	- attacker can read configs of other apps

Single point of compromise.

---
AFTER

                    SERVER
------------------------------------------------

 Apache Process 1 ---> runs as hruser
 Apache Process 2 ---> runs as ecommerce
 Apache Process 3 ---> runs as payroll
 Apache Process 4 ---> runs as inventory

------------------------------------------------

/var/www/hruser
/var/www/ecommerce
/var/www/payroll
/var/www/inventory

Now 
	- each application  has isolated permissions
	- applications cannot access each other
	- security becomes stronger
	- auditing becomes easier


---
	
### Solution :
	- Undestand Requirement 
	- Create a Linux user named ammar
	- Set custom UID as 1422
	- Set home directory as /var/www/ammar
	- Perform this on App Server 2


### Steps : 
	sudo useradd -u 1422 -d /var/www/ammar -m ammar
	
	grep ammar /etc/passwd
	ls -ld /var/www/ammar




For security hardening, instead of running Apache with default users, we can create a dedicated non-login service account and group. Then we assign ownership of web directories and configure Apache to run under that custom user. This follows the principle of least privilege and improves isolation and security.


Explanation : 

1 Running each web application with its own Linux user improves security isolation and reduces blast radius during compromise. If one application is exploited, attacker access remains restricted to that application’s files and permissions instead of the entire web server environment.

2 Custom UIDs are useful for identity consistency across shared storage, containers, and distributed systems. Using /var/www as the home directory aligns with standard Linux web hosting architecture where application content is typically stored and served by Apache or nginx.

3 In enterprise environments, running multiple applications under a shared Apache user like www-data creates security and permission risks.

4 To improve isolation and enforce least privilege access, organizations create dedicated Linux users per application.

Each application gets:
	* its own UID
	* isolated home directory
	* restricted file permissions

This prevents one compromised application from accessing another application's files or processes.

The custom Apache user typically owns the application directory under /var/www, and Apache or related services run with controlled permissions tied to that user.

This improves:
	* security isolation
	* auditing
	* compliance
	* operational maintainability

For example:
	sudo useradd -u 1029 -d /var/www/javed -m javed

This command:
	* creates the user
	* assigns a fixed UID
	* creates a dedicated application directory
	* enables controlled ownership and permission management
