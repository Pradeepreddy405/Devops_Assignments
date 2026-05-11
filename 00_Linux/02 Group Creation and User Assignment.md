## 2 Group Creation and User Assignment

### Explanation
- In Linux, groups are used to simplify permission management and enforce access control at scale.

- Instead of assigning permissions individually to every user, organizations assign permissions to groups and add users into those groups. This improves security, scalability, and operational efficiency.

- For example, in production environments different teams like HR, Finance, Developers, and DevOps require different levels of access. By creating dedicated groups, we can isolate resources and ensure users only access what they need.

- This follows the principle of least privilege and reduces security risks such as unauthorized access or accidental modification of critical files.


( or )

- Linux groups are a scalable access-control mechanism used to implement role-based permission management across users, applications, and operational teams.

- In enterprise environments, groups reduce administrative overhead, enforce least-privilege access, and isolate workloads between departments or services. They are heavily used in DevOps for managing deployment access, shared resources, logs, CI/CD permissions, and application ownership.



### Solution 
#### Step 1: Check Group Exists,if not create a group name 
	- getent group  nautilus_admin_users			---check group		
	- sudo groupadd nautilus_admin_users			---Group creation

#### Step 2:	Verify User Exists, if not exists create a user id
	- id kano										---check id
	- sudo useradd kano							---Creating the new Userid "kano"

#### Step 3:	Verify User Already in Group
	- groups kano or id kano 						---Command tell you existed groups

#### Step 4: Add User to Group
	- sudo usermod -aG nautilus_admin_users kano
	
#### Step 5: Final Verification
	- id kano
	- Expected Output : uid=1002(kano) gid=1002(kano) groups=1002(kano),1005(nautilus_admin_users)







#### One line commands
 - getent group nautilus_admin_users || sudo groupadd nautilus_admin_users
 - id kano &>/dev/null || sudo useradd kano
 - id -nG kano | grep -qw nautilus_admin_users || sudo usermod -aG nautilus_admin_users kano