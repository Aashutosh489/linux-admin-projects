Linux File/Directory Permissions
================================
Permissions in Linux control who can access a file or directory and what actions they can perform.
Permissions apply on:
1. File → control who can read, write, or execute a file.
2. Directory → control who can list contents, create files, delete files, or enter into it.
Types of Permissions:
---------------------
1. Category Permission – Basic read, write, execute permissions for users.
2. Special Permission – Includes SUID, SGID, Sticky Bit (for advanced control).
3. File Access Control Permission (ACLs) – More fine-grained permissions beyond
owner/group/others.
4. Extended Attributes – Store additional metadata about files (like SELinux labels).
Category Permission:
--------------------
Each file/directory has three categories of users:
- Owner (u) → The person who created the file.
- Group (g) → Members of the file’s group.
- Others (o) → Everyone else.
Each category can have three types of permissions:
- r = 4 → Read (view file content, list directory).
- w = 2 → Write (edit file, create/delete files in directory).
- x = 1 → Execute (run a file/script, enter a directory).
Two Modes of Setting Permissions:
---------------------------------
1. Numeric Mode (Octal Mode)
- r = 4, w = 2, x = 1
- Add the values for each category.
Example:
chmod 700 filename
Owner → 7 (rwx)
Group → 0 (---)
Others → 0 (---)
2. Symbolic Mode
- u = owner, g = group, o = others
- + = add permission, - = remove permission, = = set exact permission
Example:
chmod u=rwx,g=rx,o=r filename
(This sets permission to 754)
Ownership & Group:
------------------
Each file has:
- Owner → person who owns the file.
- Group → group of users who share access.
Change ownership:
chown ownername filename
Change group:
chgrp groupname filename
Default File/Directory Permissions:
-----------------------------------
When a file/directory is created, Linux applies a default permission, then adjusts it using umask.
- Directory default = 777 (full access)
- File default = 666 (read & write only, no execute)
umask (user mask) removes permissions:
- Common umask value = 0022
Example:
0777 (dir) - 0022 = 0755
0666 (file) - 0022 = 0644
So by default:
- Directories → 755
- Files → 644
Changing umask:
---------------
- Temporary (current shell only):
umask 0027

- Permanent (for all users):
Edit the file: /etc/profile


:Linux Special Permissions 
Normally, we have:

 r = read
 w = write
 x = execute
But Linux also has 3 special permissions:
1. Setuid (Set User ID)
2. Setgid (Set Group ID)
3. Sticky Bit

1 Setuid (Set User ID)

When applied to a file, it allows any user to run the file with the file owner’s 
permission.
 Commonly used on programs that need root power (like /usr/bin/passwd).
Example:
ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 54256 Aug 7 12:34 /usr/bin/passwd
 Notice s in owner’s execute place (rws).
 Means: even a normal user can run passwd as root (file owner).
Symbolic:
`chmod u+s filename`
Numeric:
 Setuid = 4
 Example:
`chmod 4755 filename`
(4 = Setuid, 755 = normal permissions)

2 Setgid (Set Group ID)

When applied to a file, it runs with the file’s group permission.
When applied to a directory, new files created inside get the same group as the directory 
(not the creator’s group).
Example:
`ls -ld mydir`
drwxr-sr-x 2 user developers 4096 Sep 24 12:00 mydir
 Notice s in group’s execute place (r-s).
 Means: files created in mydir will belong to developers group.
Symbolic:
`chmod g+s mydir`
Numeric:
 Setgid = 2
 Example:
 `chmod 2755 mydir`

3 Sticky Bit

Mostly used on shared directories like /tmp.
It means: only the owner of a file can delete/rename it, even if others have write 
permission on the directory.
Example:
`ls -ld /tmp`
drwxrwxrwt 10 root root 4096 Sep 24 12:05 /tmp
 Notice t at the end (rwt).
 Means: Only file owners can delete their own files.
Symbolic:
`chmod +t mydir`
Numeric:
 Sticky bit = 1
 Example:
 `chmod 1777 mydir`
🧮Quick Numeric Summary
 Setuid = 4xxx
 Setgid = 2xxx
 Sticky = 1xxx
For example:
 4755 → Setuid + normal 755
 2755 → Setgid + normal 755
 1777 → Sticky + normal 777

: So in short:

 Setuid = run as file owner
 Setgid = run as file group (or inherit group in directories)
 Sticky = only ownerr can delete own files
