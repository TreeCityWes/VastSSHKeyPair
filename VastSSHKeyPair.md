# WSL Setup and SSH Key Generation Guide

This guide walks through the process of setting up the Windows Subsystem for Linux (WSL) and generating an SSH key pair for secure connection.

## 1. Install WSL - Windows Subsystem for Linux

### a. Open PowerShell as Admin

Start by opening a PowerShell session with administrative privileges.

### b. Run Command

```sh
wsl --install
This command will enable the necessary optional features, download and install the latest Linux kernel, set WSL 2 as the default, and install a Ubuntu distribution. If you prefer a different distribution or want to install it manually, you can skip this command and follow the next steps.

c. Reboot Your Computer
After the installation finishes, reboot your computer to complete the setup.

2. Log into WSL and Create Key Pair
a. Open WSL
Open PowerShell as Admin and run:

sh
Copy code
wsl
b. Go to Root Directory
Change to the root directory by typing:

sh
Copy code
cd
c. Generate the Key Pair
Run the command to generate the key pair:

sh
Copy code
ssh-keygen -t rsa -b 4096
The -t option specifies the type of key to create (in this case, RSA).
The -b option specifies the key length (4096 bits is a good default for RSA).
You'll be asked to provide a file in which to save the key pair. Press Enter to accept the default location.
You'll be asked to enter a passphrase. This is optional — press Enter twice to skip.
Your public and private keys are now saved in WSL at \\wsl.localhost\Ubuntu\root\.ssh.
d. Add Public Key to Vast.ai
View the public key in WSL by running the command:
sh
Copy code
cat ~/.ssh/id_rsa.pub
Log into Vast.ai and click on "Account".
Locate "SSH Public Key" and paste your public key from WSL. Make sure to include the full string, including the machine name at the end.
e. Log into Your Instance
Click on "Instances" in Vast.ai.
Click on the blue "Connect" button.
Copy your connection address, for example:
sh
Copy code
ssh -p 58979 root@211.21.106.84 -L 8080:localhost:8080
Add the -i command with the path of the private key:
sh
Copy code
-i ~/.ssh/id_rsa
For example:

sh
Copy code
ssh -i ~/.ssh/id_rsa -p 58979 root@211.21.106.84 -L 8080:localhost:8080
f. Success
You are now connected to your Vast.ai instance. Enjoy your seamless and secure connection! :) """
