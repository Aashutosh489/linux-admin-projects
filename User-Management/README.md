## THIS PROJECT DEMONSTRATES LINUX USER AND GROUP MANAGEMENT BY USING COMMANDS
 
* STEPS FOR MANAGE USER ACCOUNT 

1) CREATE USER ACCOUNT  

 # useradd AASHUTOSH

2) SET USER PASSWORD

 # passwd AASHUTOSH

3) DELETE USER ACCOUNT 

 # userdel -r AASHUTOSH

4) LOCK USER PASSWORD

 # usermod -L AASHUTOSH

5) UNLOCK USER PASSWORD

 # usermod -U AASHUTOSH

6) SET USER COMMENT LINE 

 # usermod -C linuxadmin AASHUTOSH

7) SEE USER ACCOUNT MAXDAY/minday/warning

 # chage -l AASHUTOSH

8) SET USER ACCOUNT MAXDAY/minday/warning

 # chage -M 60 -m 20 -W 2 AASHUTOSH

9) SEE USER ACCOUNT PROPERTY 
 
 # cat /etc/passwd or grep AASHUTOSH /etc/passwd

10)SEE USER PASSWD PROPERTY

 # cat /etc/shadow or grep AASHUTOSH /etc/passwd

11) HOW TO ADD GROUP IN A SYSTEM

 # groupadd linuxadmin 

12) ADD MULTIPLE USER ON GROUP

 # gpasswd -M AASHUTOSH,RITIK,SHARMA linuxadmin

13) MAKE GROUP ADMIN

 # gpasswd -A AASHUTOSH linuxadmin

14) CHECK GROUP PROPERTY  

 # cat /etc/group or grep linuxadmin /etc/group

15) CHECK GROUP ADMIN PROPERTY

 # cat /etc/gshadow or grep linuxadmin /etc/gshadow

16) ADD USER ON A GROUP

 # usermod -ag linuxadmin AASHUTOSH


 
 
