# WSL Setup and SSH Key Generation Guide

Vast requires a public/private key-pair to log into your gpu instance. This guide walks through the process of setting up the Windows Subsystem for Linux (WSL) and generating an SSH key pair for a secure connection to Vast.ai instances. 

## 1. Install WSL - Windows Subsystem for Linux

- **Open PowerShell as Admin**: Start by opening a PowerShell session with administrative privileges.

- **Run Command**: 
    ```sh
    wsl --install
    ```
    This command will enable the necessary features, download and install the latest Linux kernel, set WSL 2 as the default, and install a Ubuntu distribution. If you prefer a different distribution or want to install it manually, you can skip this command and follow the next steps.

- **Reboot Your Computer**: After the installation finishes, reboot your computer to complete the setup.

## 2. Log into WSL and Create Key Pair

- **Open WSL**: Open PowerShell as Admin and run:
    ```sh
    wsl
    ```

- **Go to Root Directory**: Change to the root directory by typing:
    ```sh
    cd
    ```

- **Generate the Key Pair**: Run the command to generate the key pair:
    ```sh
    ssh-keygen -t rsa -b 4096
    ```
    - The `-t` option specifies the type of key to create (in this case, RSA).
    - The `-b` option specifies the key length (4096 bits is a good default for RSA).
    - You'll be asked to provide a file in which to save the key pair. Press Enter to accept the default location.
    - You'll be asked to enter a passphrase. This is optional — press Enter twice to skip.
    - Your public and private keys are now saved in WSL at `\\wsl.localhost\Ubuntu\root\.ssh`.

- **Set Correct Permissions for Private Key**:
    After generating your key pair, it's important to set the correct permissions on your private key file. This is a security measure required by SSH. Run the following command:
    
    ```sh
    chmod 400 ~/.ssh/id_rsa
    ```

- **Add Public Key to Vast.ai**:
    1. View the public key in WSL by running the command:
        ```sh
        cat ~/.ssh/id_rsa.pub
        ```
    2. Log into Vast.ai and click on "Account".
    3. Locate "SSH Public Key" and paste your public key from the WSL command above into Vast.ai and save. Make sure to include the full string, including the machine name at the end. Make sure Vast.ai confirms it's a valid key. 

- **Log into Your Instance**:
    1. Click on "Instances" in Vast.ai.
    2. Click on the blue "Connect" button.
    3. Copy your connection address, for example:
        ```sh
        ssh -p 58979 root@211.21.106.84 -L 8080:localhost:8080
        ```
    4. Add the `-i` command with the path of the private key:
        ```sh
        -i ~/.ssh/id_rsa
        ```
        For example:
        ```sh
        ssh -i ~/.ssh/id_rsa -p 58979 root@211.21.106.84 -L 8080:localhost:8080
        ```

- **Success**: You are now connected to your Vast.ai instance. Enjoy your seamless and secure connection! :)
