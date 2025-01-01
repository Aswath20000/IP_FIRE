SSH Reverse Shell IPFire
----------------------------

This repository provides the necessary instructions and scripts to establish a secure SSH reverse shell for IPFire. This setup is particularly useful for gaining remote access to an IPFire system in scenarios where inbound connections are restricted.

Features
-----------------------------------

• Establishes a reverse shell connection via SSH.

• Designed for secure and controlled remote access.

• Compatible with IPFire installations.


Prerequisites
------------------------------------


• An IPFire system that is installed and properly configured.

• A server with SSH enabled to accept reverse shell connections.

• Dependencies including OpenSSH and basic Linux utilities like `curl` or `wget`.

Installation
----------------------------------------------
 

# Install and Configure SSH on IPFire 

apt-get update 

apt-get install openssh-server 

nano /etc/ssh/sshd_config 

PermitRootLogin yes 

PasswordAuthentication yes 

service sshd restart 

  

# Install SSH Client on Device A and Device B 

apt-get update 

apt-get install openssh-client 

  

# Assign Static IPs to IPFire Interfaces 

ip addr add 192.168.1.1/24 dev eth0 

ip addr add 203.0.113.1/24 dev eth1 

  

# Enable SSH Access on IPFire 

nano /etc/ssh/sshd_config 

PermitRootLogin yes 

PasswordAuthentication yes 

service sshd restart 

  

# Configure Port Forwarding on IPFire 

1. Access the IPFire web interface. 

2. Navigate to Firewall > Port Forwarding. 

3. Add a rule with: 

      Source: Any 

      Destination: IPFire RED IP 

      Protocol: TCP 

      Destination Port: 22 

  

 

# Add Firewall Rules on IPFire 

1. Navigate to Firewall > Rules. 

2. Add a rule with: 

     Action: Allow 

      Protocol: TCP 

     Source Zone: GREEN 

     Destination Zone: RED 

     Port: 22 

  

# Establish Reverse SSH on Device A 

ssh-keygen -t rsa 

ssh-copy-id user@<IPFire_IP> 

ssh -R 2222:localhost:22 user@<IPFire_IP> 

  

# Connect to Device A from Device B 

ssh-keygen -t rsa 

ssh-copy-id user@<IPFire_IP> 

ssh -p 2222 user@<IPFire_IP> 

  

 

 
