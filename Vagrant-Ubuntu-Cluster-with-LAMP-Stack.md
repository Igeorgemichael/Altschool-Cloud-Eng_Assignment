# [Assigment]()
- ## Project Task: 
  - **Deployment of Vagrant Ubuntu Cluster with LAMP Stack**

- ## Objective:
  - Develop a bash script to orchestrate the automated deployment of two Vagrant-based Ubuntu systems, designated as `Master` and `Slave`,
  - Provision an integrated LAMP stack on both systems.

- ## Specifications:
  - Infrastructure Configuration:
  - Deploy two Ubuntu systems:
  - Master Node: This node should be capable of acting as a control

- ## User Management:
     On the `Master node`:
  - Create a user named altschool.
  - Grant altschool user root (superuser) privileges.

- ## Inter-node Communication:
     Enable SSH key-based authentication:      
     The Master node (altschool user) should seamlessly SSH into the Slave node without requiring a password.

- ## Data Management and Transfer:
     On initiation:
  - Copy the contents of /mnt/altschool directory from the Master node to /mnt/altschool/slave on the Slave node.
  - This operation should be performed using the altschool user from the Master node.

- ## Process Monitoring:
  - The Master node should display an overview of the Linux process management,
  - showcasing currently running processes.

- ## LAMP Stack Deployment:
     Install a AMP (Apache, MySQL, PHP) stack on both nodes:
  - Ensure Apache is running and set to start on boot.
  - Secure the MySQL installation and initialize it with a default user and password.
  - Validate PHP functionality with Apache.

---
## [Deliverables:]()

- ## Step 1: Set Up Your Environment
  - You'll make a provisioning for a Hypervisor Install VirtualBox
  - You will need to Install Vagrant on your Work-Station
  - Create a project directory for your Vagrant configuration and bash script
  - Make the bash script executable by running this command **`chmod +x vagrant-lamp.sh`**

- ## Step 2: Creating Two Vagrant Ubuntu Machine
  - run the command to call up the file and the script
    ``` bash
    vim vagrant-lamp.sh 
    ```
  - In the provisioning script add the code line to configure  **Master Machine** [Germany]
![slave-machine](https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/ca3fdd60-3b11-4080-9c42-bc7b515e3b41)

  - also add the code line to the script to configure **Slave Machine** [Moscow]
![master-machine](https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/0db76442-a765-4314-abd7-c16551fd182d)

- ### Below is the Configuration Script for the creation of both Master and Slave Machine

``` bash
#!/bin/bash

vagrant init ubuntu/focal64

cat <<EOF>>Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.define "moscow" do |moscow|
    moscow.vm.hostname = "moscow"
    moscow.vm.box = "ubuntu/focal64"
    moscow.vm.network "private_network", ip: "192.168.56.11"

    moscow.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update && sudo apt-get upgrade -y
     sudo apt install sshpass -y
     sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
     sudo systemctl restart sshd
     sudo apt-get install -y avahi-daemon libnss-mdns
    SHELL
  end

  config.vm.define "germany" do |germany|
    germany.vm.hostname = "germany"
    germany.vm.box = "ubuntu/focal64"
    germany.vm.network "private_network", ip: "192.168.56.10"

    germany.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update && sudo apt-get upgrade -y
     sudo apt-get install -y avahi-daemon libnss-mdns
     sudo apt install sshpass -y
     # sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
     # sudo systemctl restart sshd
    SHELL
  end

    config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "2"
    end
end
EOF

vagrant up

source provision.sh
```
  - Save and exit the Vim Editor by pressing the escape key on the keyboard then run this command:
    **`:wq`**

- ## Step 3: How To Enable SSH Key

- To enable SSH key authentication on the master and slave nodes in Vagrant.   
  - Generate an SSH key pair on the master node. You can do this by running this command in the terminal:   `ssh-keygen -t rsa -b 4096`

  - This will generate a private key `id_rsa` and a public key `id_rsa.pub`.    
    - Copy the public key to the slave node. You can do this by running the following command in the terminal:
ssh-copy-id slave

  Enable SSH key authentication on the slave node. To do this, edit the `/etc/ssh/sshd_config` file on the slave node and change the `PasswordAuthentication` setting to `no`.    
  Restart the SSH service on the slave node. You can do this by running the following command in the terminal:   
   ```
    sudo service ssh restart
   ```

- ## Step 4: How To Install The LAMP Provision
  How to install LAMP stack on both master and slave vagrant file

  -  Linux
  -  Apache
  -  MySQL
  -  PHP

Combining these components on an Ubuntu system creates a powerful environment for web development and hosting. Developers can build web applications using PHP and connect them to MySQL databases, while Apache handles the web server aspects, ensuring that web pages are served to clients' browsers.

  - before installing the provisioning, let's make sure that our package repo is not in a stale state
  - run the command to update the repo, then proceed with the provisioning.






































