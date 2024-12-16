# saturnrings-server
Instructions and some handy notes to setup a home server and connect using SSH. 

### Referred articles :: 
1. https://dev.to/zduey/how-to-set-up-an-ssh-server-on-a-home-computer
2. https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys
3. https://gcore.com/learning/how-to-change-ssh-port/

### Learning material :: 
1. https://www.codecademy.com/learn/learn-the-command-line

### Few useful info about my machine :: 
OS :: Debian 12
Hardware :: Intel i7
RAM :: 8 gigs
SSD :: 500 gigs
Graphics (I don't think its relavant) :: Nvidia GEFORCE 940mx

### Steps I followed to access my home server remotely using SSH

1. Update your system packages
```
sudo apt-get upgrade
```
2. Install openssh-client and openssh-server
```
sudo apt-get install openssh-client
sudo apt-get install openssh-server
```
3. You should now have an SSH server process running on your machine. Check with the following:
```
ps -A | grep sshd
```
4. Optional step :: Change the default ssh port from 22 to something else. Ref link 3
   
   <details>
   <summary>Expand</summary>

   a. Backup the Configuration File. Before making any changes, it’s always a good practice to back up your SSH configuration file.
   ```
   sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
   ```
   b. Edit the SSH Configuration File. Open the SSHD configuration file with your preferred text editor. For this example, we’ll use nano.
   ```
   sudo nano /etc/ssh/sshd_config
   ```
   c. Locate the Port Directive. Find the line that starts with Port. It should say Port 22 by default.
   d. Change the Port Number. Edit the line to reflect your desired port number, preferably above 1024 to avoid conflicts with other standard services. For instance, to change it to port 2222, the line would look like:
   ```
   Port 2222
   ```
   e. Restart the SSH Service. Apply the changes by restarting the SSH daemon.
   ```
   sudo systemctl restart sshd
   ```
   f. Test the New SSH Port. Before logging out of your current session, open a new terminal or SSH client and try connecting to the server using the new port to ensure everything works correctly:
   ```
   ssh username@your_server_ip -p 2222
   ```
   </details>
#### Generating and Working with SSH Keys (Ref article 2) ::
5. Generating a new SSH public and private key pair on your local computer is the first step towards authenticating with a remote server without a password. Unless there is a good reason not to, you should always authenticate using SSH keys.
A number of cryptographic algorithms can be used to generate SSH keys, including RSA, DSA, and ECDSA. RSA keys are generally preferred and are the default key type.
To generate an RSA key pair on your local computer, type:
```
ssh-keygen
```
```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/demo/.ssh/id_rsa):
```
This prompt allows you to choose the location to store your RSA private key. Press ENTER to leave this as the default, which will store them in the .ssh hidden directory in your user’s home directory. Leaving the default location selected will allow your SSH client to find the keys automatically.
```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
The next prompt allows you to enter an arbitrary length passphrase to secure your private key. As an additional security measure, you will have to enter any passphrase you set here every time you use the private key. Feel free to press ENTER to leave this blank if you do not want a passphrase. Keep in mind, though, that this will allow anyone who gains control of your private key to log in to your servers.

If you choose to enter a passphrase, nothing will be displayed as you type. This is a security precaution.
```
Output
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
8c:e9:7c:fa:bf:c4:e5:9c:c9:b8:60:1f:fe:1c:d3:8a root@here
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|                 |
|       +         |
|      o S   .    |
|     o   . * +   |
|      o + = O .  |
|       + = = +   |
|      ....Eo+    |
+-----------------+
```
This procedure has generated an RSA SSH key pair located in the .ssh hidden directory within your user’s home directory. These files are:

~/.ssh/id_rsa: The private key. DO NOT SHARE THIS FILE!
~/.ssh/id_rsa.pub: The associated public key. This can be shared freely without consequence.

6. Copying your Public SSH Key to a Server with SSH-Copy-ID
To copy your public key to a server, allowing you to authenticate without a password, a number of approaches can be taken.

If you currently have password-based SSH access configured to your server, and you have the ssh-copy-id utility installed, this is a simple process. The ssh-copy-id tool is included in many Linux distributions’ OpenSSH packages, so it very likely may be installed by default.

If you have this option, you can easily transfer your public key by typing:
```
ssh-copy-id username@remote_host
```
This will prompt you for the user account’s password on the remote system:
```
The authenticity of host '111.111.11.111 (111.111.11.111)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
demo@111.111.11.111's password:
```
After typing in the password, the contents of your ~/.ssh/id_rsa.pub key will be appended to the end of the user account’s ~/.ssh/authorized_keys file:
```
Output
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'demo@111.111.11.111'"
and check to make sure that only the key(s) you wanted were added.
```
You can now log in to that account without a password:
```
ssh username@remote_host
```
7. Copying your Public SSH Key to a Server Without SSH-Copy-ID - Ref link :: https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys#copying-your-public-ssh-key-to-a-server-without-ssh-copy-id
8. 






