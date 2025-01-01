
# SSH Reverse Shell for IPFire

This repository provides the necessary instructions and scripts to establish a secure SSH reverse shell for IPFire. This setup is particularly useful for gaining remote access to an IPFire system in scenarios where inbound connections are restricted.

## Features

- Establishes a reverse shell connection via SSH.
- Designed for secure and controlled remote access.
- Compatible with IPFire installations.

## Prerequisites

- An IPFire system that is installed and properly configured.
- A server with SSH enabled to accept reverse shell connections.
- Dependencies including OpenSSH and basic Linux utilities like `curl` or `wget`.

## Installation

### Install and Configure SSH on IPFire

```bash
apt-get update
apt-get install openssh-server
nano /etc/ssh/sshd_config
# Ensure the following configurations are set:
PermitRootLogin yes
PasswordAuthentication yes
service sshd restart
```

### Install SSH Client on Device A and Device B

```bash
apt-get update
apt-get install openssh-client
```

### Assign Static IPs to IPFire Interfaces

```bash
ip addr add 192.168.1.1/24 dev eth0
ip addr add 203.0.113.1/24 dev eth1
```

### Enable SSH Access on IPFire

```bash
nano /etc/ssh/sshd_config
# Ensure the following configurations are set:
PermitRootLogin yes
PasswordAuthentication yes
service sshd restart
```

### Configure Port Forwarding on IPFire

1. Access the IPFire web interface.
2. Navigate to **Firewall > Port Forwarding**.
3. Add a rule with:
   - **Source**: Any
   - **Destination**: IPFire RED IP
   - **Protocol**: TCP
   - **Destination Port**: 22

### Add Firewall Rules on IPFire

1. Navigate to **Firewall > Rules**.
2. Add a rule with:
   - **Action**: Allow
   - **Protocol**: TCP
   - **Source Zone**: GREEN
   - **Destination Zone**: RED
   - **Port**: 22

### Establish Reverse SSH on Device A

```bash
ssh-keygen -t rsa
ssh-copy-id user@<IPFire_IP>
ssh -R 2222:localhost:22 user@<IPFire_IP>
```

### Connect to Device A from Device B

```bash
ssh-keygen -t rsa
ssh-copy-id user@<IPFire_IP>
ssh -p 2222 user@<IPFire_IP>
```

## Conclusion

This guide provides a comprehensive approach to establishing a secure SSH reverse shell for IPFire. By following the outlined steps, users can enable remote access in environments with restricted inbound connections while maintaining security and control. Proper configuration and adherence to best practices are critical for ensuring a secure setup.

## References

1. IPFire Official Documentation: [https://www.ipfire.org/docs](https://www.ipfire.org/docs)
2. OpenSSH Documentation: [https://www.openssh.com/manual.html](https://www.openssh.com/manual.html)

## License

This project is licensed under the MIT License. See the details below:

```
MIT License

Copyright (c) 2025 [Your Name or Organization]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
