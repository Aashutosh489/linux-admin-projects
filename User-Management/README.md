# Linux User Management via CLI
A hands-on demonstration of Linux user and group management using command-line tools. Ideal for system administrators and support engineers.

## 🔍 Project Outcome
- Created and managed user accounts using CLI tools
- Demonstrated secure password handling and account lifecycle
- Useful for onboarding automation and server access control

markdown table

1) create user account  

 # useradd AASHUTOSH

2) set user passwd

 # passwd AASHUTOSH

3) delete user account 

 # userdel -r AASHUTOSH

4) lock user passwd

 # usermod -L AASHUTOSH

5) unlock user passwd

 # usermod -U AASHUTOSH

6) set user comment line

 # usermod -C linuxadmin AASHUTOSH

7) see user account maxday/minday/warning

 # chage -l AASHUTOSH

8) set user account maxday/minday/warning

 # chage -M 60 -m 20 -W 2 AASHUTOSH

9) see user account property
 
 # cat /etc/passwd or grep AASHUTOSH /etc/passwd

10) see user passwd property

 # cat /etc/shadow or grep AASHUTOSH /etc/passwd

11) add group in a system

 # groupadd linuxadmin 

12) add multiple user on group

 # gpasswd -M AASHUTOSH,RITIK,SHARMA linuxadmin

13) make group admin

 # gpasswd -A AASHUTOSH linuxadmin

14) check group property

 # cat /etc/group or grep linuxadmin /etc/group

15) check group admin property 

 # cat /etc/gshadow or grep linuxadmin /etc/gshadow

16) add user on a group 

 # usermod -ag linuxadmin AASHUTOSH


 
 
