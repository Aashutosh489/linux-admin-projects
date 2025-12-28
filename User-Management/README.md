# Linux User Management via CLI
A hands-on demonstration of Linux user and group management using command-line tools. Ideal for system administrators and support engineers.

## 🔍 Project Outcome
- Created and managed user accounts using CLI tools
- Demonstrated secure password handling and account lifecycle
- Useful for server access control

Linux User Management

1. What is User Management?

In Linux, everything is multi-user. User management is the process of creating, modifying, and
deleting users and groups, and controlling their access to system resources. It ensures security,
accountability, and controlled access.

2. Types of Users

1. Root user → Superuser, has full privileges.
2. System users → Created by the OS or applications (e.g., apache, mysql).
3. Normal users → Created for human users.

3. User Management Commands

• Create user: useradd username
• Set password: passwd username
• Modify user: usermod -aG group username
• Delete user: userdel -r username
• View user info: id username | whoami | groups username

4. Important Configuration Files

a) /etc/passwd
Stores user account information. Each line has 7 fields:
username:x:UID:GID:comment:home_directory:shell
b) /etc/shadow
Stores encrypted passwords and password policies. Each line has 9 fields:
username:password:lastchg:min:max:warn:inactive:expire:reserved
c) /etc/group
Stores group information. Format:
group_name:password:GID:user_list
d) /etc/gshadow
Stores secure group passwords.
e) /etc/login.defs
Defines default UID range, password policy, and umask.
f) /etc/skel/
Contains default files copied into a new user’s home directory.

5. Account Security

• Lock account: usermod -L username
• Unlock account: usermod -U username
• Expire account: chage -E YYYY-MM-DD username
• Check password aging: chage -l username

6. User Expiry & Password Aging

a) Checking Expiry Date
Use: chage -l username
Shows last password change, expiry date, and aging policies.
b) Setting Expiry Date
Use: usermod -e YYYY-MM-DD username
Example: usermod -e 2025-12-31 rahul
c) Removing Expiry Date
Use: usermod -e "" username
d) Password Aging
Use: chage -M 90 -m 7 -W 14 username
-M: Maximum days
-m: Minimum days
-W: Warning before expiry
Alternative: passwd -x 90 -n 7 -w 14 username
e) Files Involved
/etc/shadow → Stores expiry info
/etc/login.defs → Default password aging policy

7. UID & GID Ranges

Each user in Linux is identified by a UID (User ID) and each group by a GID (Group ID).
• UID 0 → root user (superuser)
• UID 1–999 → System/service accounts (e.g., daemon, mysql)
• UID 1000+ → Normal users
• GID follows the same ranges for groups
You can check ranges in /etc/login.defs:
UID_MIN 1000
UID_MAX 60000
GID_MIN 1000
GID_MAX 60000
Example from /etc/passwd:
root:x:0:0:root:/root:/bin/bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/sbin/nologin
rahul:x:1000:1000:Rahul Sisodiya:/home/rahul:/bin/bash
Example from /etc/group:
root:x:0:
wheel:x:10:root
docker:x:998:
rahul:x:1000:

8. Basic User Modification Commands

1. Change Username: usermod -l newname oldname
2. Change Home Directory: usermod -d /new/home/dir username (with -m to move
files)
3. Change Login Shell: usermod -s /bin/zsh username
4. Add User to a Group: usermod -aG groupname username
5. Change Primary Group: usermod -g groupname username
6. Lock/Unlock Account: usermod -L/-U username
7. Set Account Expiry: usermod -e YYYY-MM-DD username
8. Change User Password: passwd username (or passwd -e username to force change
at next login)
9. Change User UID: usermod -u 1050 username


1) create user account  

 `useradd AASHUTOSH`

2) set user passwd

 `passwd AASHUTOSH`

3) delete user account 

 `userdel -r AASHUTOSH`

4) lock user passwd

 `usermod -L AASHUTOSH`

5) unlock user passwd

 `usermod -U AASHUTOSH`

6) set user comment line

 `usermod -C linuxadmin AASHUTOSH`

7) see user account maxday/minday/warning

 `chage -l AASHUTOSH`

8) set user account maxday/minday/warning

 `chage -M 60 -m 20 -W 2 AASHUTOSH`

9) see user account property
 
 `cat /etc/passwd or grep AASHUTOSH /etc/passwd`

10) see user passwd property

 `cat /etc/shadow or grep AASHUTOSH /etc/passwd`

11) add group in a system

  `groupadd linuxadmin`

12) add multiple user on group

  `gpasswd -M AASHUTOSH,RITIK,SHARMA linuxadmin`

13) make group admin

  `gpasswd -A AASHUTOSH linuxadmin`

14) check group property

  `cat /etc/group or grep linuxadmin /etc/group`

15) check group admin property 

  `cat /etc/gshadow or grep linuxadmin /etc/gshadow`

16) add user on a group 

  `usermod -ag linuxadmin AASHUTOSH`


 
 
