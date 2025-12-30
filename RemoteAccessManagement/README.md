📌Remote Access Management in Linux

1. What is Remote Access?

 Remote access means connecting to a Linux system from another computer
over a network (LAN or Internet).

 Example: You are at home and want to log in to your office Linux server.

2. Why Remote Access is Important?

 Manage servers without being physically there.

 Transfer files.

 Run commands and monitor system health.

 Provide support to users remotely.

3. Common Remote Access Tools in Linux

a) SSH (Secure Shell)

 Most common tool for remote login.

 Secure (encrypted) communication.

 Command:
 ssh username@server_ip

 Example:
 ssh rahul@192.168.1.10

→ This logs in as user rahul on server 192.168.1.10.

b) SCP (Secure Copy)

 For copying files between local and remote.

 Example: Copy a file from local to server:

 scp file.txt rahul@192.168.1.10:/home/rahul/

c) FTP (File Transfer Protocol)

 Not secure.

 Connect using:
 ftp rahul@192.168.1.10

 Then you can use commands like put (upload) and get (download).

d) Telnet (Not Recommended)

 Old method, not secure (no encryption).

 Use only for learning, not in production.

4. Configuring Remote Access

a) SSH Server Installation

 Install SSH server:

 sudo apt install openssh-server # Ubuntu/Debian

 sudo yum install openssh-server # CentOS/RHEL

 Start the service:

 sudo systemctl start sshd

 sudo systemctl enable sshd

b) Configuration File

 Location: /etc/ssh/sshd_config

 Key options:
o Port 22 → Default SSH port .

o PermitRootLogin no → Disable root login for security.

Restart SSH after changes:
systemctl restart sshd

6. Real Life Example

 Secure with SSH keys, firewall, disable root.
Password Less Login

📌SSH Key-Based Authentication (Password-less Login)

1. What are SSH Keys?

 Instead of typing a password every time, you can use SSH keys.

 It uses two keys:

o Private Key (kept secret on your computer).

o Public Key (shared with the server).
Think of it like a lock and key:

 The public key is like a lock installed on the server.

 The private key is like your personal key that opens the lock.

2. Generate SSH Key Pair

Run this command on your local machine (client):
ssh-keygen

 It will ask where to save the key (default: ~/.ssh/id_rsa).

 Press Enter to accept default.

 It creates two files:

o id_rsa → Private Key (keep safe, don’t share).

o id_rsa.pub → Public Key (can be shared).

3. Copy Public Key to Server

Use this command to copy your public key:

ssh-copy-id username@server_ip

Example:
ssh-copy-id rahul@192.168.1.10

This command puts your public key into the server file:
~/.ssh/authorized_keys

4. Login Without Password

Now try logging in:
ssh rahul@192.168.1.10

5. Security Notes

 Never share your private key.

 You can add a passphrase for extra protection when generating the key.

 Only the public key should be copied to servers.

6. Real Life Example

1. At home, you generate SSH keys.

2. You copy the public key to your office server.

3. Next time you run:

4. ssh admin@203.0.113.25
You get logged in instantly, no password needed.

✅Updated Training Summary:

 SSH = secure remote access.

 SCP/SFTP = file transfers.

 Configure /etc/ssh/sshd_config.

 Secure with SSH keys.

 Use ssh-keygen + ssh-copy-id for password-less login.

 Disable root login, change port, use firewall.

📌Where SSH Public Key is Stored

When you run:

ssh-copy-id user@server_ip

It copies your public key (id_rsa.pub) to the server and saves it inside this file:
/home/username/.ssh/authorized_keys

 authorized_keys can store multiple public keys (one per line).

 Each line = one user’s public key that is allowed to log in.
Example of authorized_keys file content:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC... user@clientPC

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQX... otheruser@laptop

 How to Delete a Stored Public Key

Step 1: Log in to the server (with password or existing key)
ssh user@server_ip

Step 2: Open the authorized_keys file
nano ~/.ssh/authorized_keys

Step 3: Find the line with your key

 Each key is usually one long line starting with ssh-rsa or ssh-ed25519.

 Delete that line.

Step 4: Save and exit

 Press CTRL+X, then Y, then Enter (in nano).
Now that public key will no longer work for login.

📌How to Deny User Access in Linux

1. Deny Using /etc/ssh/sshd_config

 SSH server config file:

 /etc/ssh/sshd_config

 Add this line to deny specific users:

 DenyUsers username
 Example:
 DenyUsers rahul
Now user rahul cannot log in via SSH.

 Or to deny multiple users:

 DenyUsers rahul sachi testuser

✅After changes, restart SSH service:

sudo systemctl restart sshd

2. Remove from authorized_keys

 If the user uses SSH keys, remove their public key from:

 ~/.ssh/authorized_keys
After removal, they must use a password. If account is locked, they cannot log in at all.
