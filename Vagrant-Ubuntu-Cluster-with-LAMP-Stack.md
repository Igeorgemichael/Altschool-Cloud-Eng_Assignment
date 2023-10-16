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

---

- ### Below is the Configuration Script for the creation of both Master and Slave Machine

``` bash
#!/bin/bash

vagrant init ubuntu/focal64

cat <<EOF >>Vagrantfile
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
---

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

- ## Step 4: User Management
  ```
   sudo useradd -m -G sudo altschool
   echo -e "michael\nmichael\n" | sudo passwd altschool
  ```
 This command creates a new user named "altschool" with the following options;        
 This option `-m` creates the user's home directory if it doesn't exist,     
 This option `-G`  sudo: adds the user to the "sudo" group, which typically grants administrative privileges. 

The second command:
This command sets the password for the "altschool"
This is used as the new password for the "altschool" user.

---

## Below is the second part of the script 
```
#!/bin/bash

vagrant ssh germany <<EOF
    sudo useradd -m -G sudo altschool
    echo -e "michael\nmichael\n" | sudo passwd altschool 
    sudo usermod -aG root altschool
    sudo useradd -ou 0 -g 0 altschool
    sudo -u altschool ssh-keygen -t rsa -b 4096 -f /home/altschool/.ssh/id_rsa -N "" -y
    sudo cp /home/altschool/.ssh/id_rsa.pub altschoolkey
    sudo ssh-keygen -t rsa -b 4096 -f /home/vagrant/.ssh/id_rsa -N ""
    sudo cat /home/vagrant/.ssh/id_rsa.pub | sshpass -p "vagrant" ssh -o StrictHostKeyChecking=no vagrant@192.168.56.11 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
    sudo cat ~/altschoolkey | sshpass -p "vagrant" ssh vagrant@192.168.56.11 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
    sshpass -p "michael" sudo -u altschool mkdir -p /mnt/altschool/moscow
    sshpass -p "michael" sudo -u altschool scp -r /mnt/* vagrant@192.168.56.11:/home/vagrant/mnt
    sudo ps aux > /home/vagrant/monitored_process
    exit
EOF

vagrant ssh germany <<EOF
echo -e "\n\nUpdating Apt Packages and upgrading latest patches\n"
sudo apt update -y

sudo apt install apache2 -y

echo -e "\n\nAdding firewall rule to Apache\n"
sudo ufw allow in "Apache"

sudo ufw status

echo -e "\n\nInstalling MySQL\n"
sudo apt install mysql-server -y

echo -e "\n\nPermissions for /var/www\n"
sudo chown -R www-data:www-data /var/www
echo -e "\n\n Permissions have been set\n"

sudo apt install php libapache2-mod-php php-mysql -y

echo -e "\n\nEnabling Modules\n"
sudo a2enmod rewrite
sudo phpenmod mcrypt

sudo sed -i 's/DirectoryIndex index.html index.cgi index.pl index.xhtml index.htm/DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm/' /etc/apache2/mods-enabled/dir.conf

echo -e "\n\nRestarting Apache\n"
sudo systemctl reload apache2

echo -e "\n\nLAMP Installation Completed"

exit 0
EOF

vagrant ssh moscow <<EOF
echo -e "\n\nUpdating Apt Packages and upgrading latest patches\n"
sudo apt update -y

sudo apt install apache2 -y

echo -e "\n\nAdding firewall rule to Apache\n"
sudo ufw allow in "Apache"

sudo ufw status

echo -e "\n\nInstalling MySQL\n"
sudo apt install mysql-server -y

echo -e "\n\nPermissions for /var/www\n"
sudo chown -R www-data:www-data /var/www
echo -e "\n\n Permissions have been set\n"

sudo apt install php libapache2-mod-php php-mysql -y

echo -e "\n\nEnabling Modules\n"
sudo a2enmod rewrite
sudo phpenmod mcrypt

sudo sed -i 's/DirectoryIndex index.html index.cgi index.pl index.xhtml index.htm/DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm/' /etc/apache2/mods-enabled/dir.conf

echo -e "\n\nRestarting Apache\n"
sudo systemctl reload apache2

echo -e "\n\nLAMP Installation Completed"

exit 0
EOF

```
---

- ## Step 5: How To Install The LAMP Provision
  How to install LAMP stack on both master and slave vagrant file

  -  Linux
  -  Apache
  -  MySQL
  -  PHP

Combining these components on an Ubuntu system creates a powerful environment for web development and hosting. Developers can build web applications using PHP and connect them to MySQL databases, while Apache handles the web server aspects, ensuring that web pages are served to clients' browsers.

  - before installing the provisioning, let's make sure that our package repo is not in a stale state
  - run the command `sudo apt update -y` to update the repo, then proceed with the provisioning.
![repo-update](https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/361afcb2-6850-4593-b2d9-ed467f385edc)
  - **Installing the provisions**
``` bash
sudo apt install apache2 -y

echo -e "\n\nAdding firewall rule to Apache\n"
sudo ufw allow in "Apache"

sudo ufw status

echo -e "\n\nInstalling MySQL\n"
sudo apt install mysql-server -y

echo -e "\n\nPermissions for /var/www\n"
sudo chown -R www-data:www-data /var/www
echo -e "\n\n Permissions have been set\n"

sudo apt install php libapache2-mod-php php-mysql -y

echo -e "\n\nEnabling Modules\n"
sudo a2enmod rewrite
sudo phpenmod mcrypt
```

- ## Step 6: Copying Mnt From One Node To Another

these commands are being used to create a directory, "moscow," on the local system and then copy the contents of the local /mnt directory to a remote system using sshpass for password authentication and scp for the file transfer. The actions are being performed with specific user privileges, which may require appropriate permissions and configuration on the remote system.

``` bash
 sshpass -p "michael" sudo -u altschool mkdir -p /mnt/altschool/moscow
 sshpass -p "michael" sudo -u altschool scp -r /mnt/* vagrant@192.168.56.11:/home/vagrant/mnt
```

- ## Step 7: Process Monitoring
  
This will execute the ps aux command with elevated privileges, and the output of that command (a list of running processes) will be saved to the file named "monitored_process" in the /home/vagrant directory. This can be useful for monitoring and capturing information about the system's running processes for analysis.

```
 sudo ps aux > /home/vagrant/monitored_process
```

- ## Step 8: Confirming Apache is Running
  Check Apache Service Status with systemctl:

  You can use the `systemctl` command to check the status of the Apache service:
 ```
 sudo systemctl status apache2
```

   - If Apache is up and running, you'll see an output that indicates it's active and running.

   - If Apache was not already running, this command will start the Apache service.
 ```
  sudo systemctl start apache2
 ```























