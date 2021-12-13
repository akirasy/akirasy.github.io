---
layout : default
grand_parent : Linux OS
parent : Software & Packages
title  : Docker
---

# {{ page.title }}
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Installation

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:
    ```
    apt-get install ca-certificates curl gnupg lsb-release
    ```
2. Create a `bash` file using this code and save as `install-docker.sh`.
    ```
    #!/usr/bin/env bash
    
    # Check sudo
    case $EUID in
        0) clear; echo -e "\n\033[1;36mSudo priviledge: Granted\033[0m\n" ;;
        *) echo -e "\n\033[1;36mInstaller must be run as sudo.\033[0m\n" 
           echo "Exiting now.\n"; exit ;;
    esac
    
    # Register docker as repository
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    # Install docker as repository
    apt update
    apt install -y docker-ce docker-ce-cli containerd.io
    
    # Post-installation steps to manage docker as non-root user
    groupadd docker
    usermod -aG docker $USER
    
    echo "Installation script completed!"
    ```
3. Execute the file using sudo.
    ```
    sudo bash install-docker.sh
    ```
4. Verify that Docker Engine is installed correctly by running the hello-world image.
    ```
    docker run hello-world
    ```
