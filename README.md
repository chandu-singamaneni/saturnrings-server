# saturnrings-server
Instructions and some handy notes to setup a home server and connect using SSH. 

### Referred articles :: 
1. https://dev.to/zduey/how-to-set-up-an-ssh-server-on-a-home-computer
2. https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys

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
4.    


