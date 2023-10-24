# [EXAM PROJECT]() 2nd Semester
### Task

- Automate the provisioning of two Ubuntu-based servers, named `Master` and `Slave`, using Vagrant.
- On the Master node, create a bash script to automate the deployment of a LAMP (Linux, Apache, MySQL, PHP) stack. 
- This script should clone a PHP application from GitHub, install all necessary packages, and configure Apache web server and MySQL.  
- Ensure the bash script is reusable and readable. 
  - Using an Ansible playbook: 
	  -	Execute the bash script on the Slave node and verify that the PHP application is accessible through the VM's IP address (take a screenshot of this as evidence) 
	  - Create a cron job to check the server's uptime every 12 a.m. 

[PHP Laravel GitHub Repository:](https://github.com/laravel/laravel)

---

## [Solution]()

- [ ] **What this repo is all about**
### Laravel: 
  Laravel is a popular open-source PHP web application framework known for its elegant syntax, developer-friendly features, and robust set of tools for building modern web applications. It was created by Taylor Otwell and first released in 2011. Laravel follows the Model-View-Controller (MVC) architectural pattern and provides a range of features to simplify and speed up web development.

### LAMP Stack:
  A LAMP stack is a popular open-source web development platform that consists of four key components, each of which plays a specific role in web application development. The term "LAMP" is an acronym that represents these four components:

- **Linux**: Linux is the operating system that forms the foundation of the LAMP stack. It provides the environment for hosting web applications and serves as the server's underlying operating system. Linux is chosen for its stability, security, and versatility.

- **Apache**: Apache is the web server software in the LAMP stack. It's responsible for handling client requests and serving web content to users' web browsers. Apache is highly configurable and supports a wide range of web-related technologies. It's known for its reliability and widespread use in the web hosting industry.

- **MySQL**: MySQL is the relational database management system (RDBMS) used in the LAMP stack for storing and managing data. It is known for its speed and reliability, making it a popular choice for web applications.

- **PHP**: PHP is the server-side scripting language that enables the dynamic generation of web content and interactions with the database. It's a powerful language for web development and is widely used for creating web applications. PHP scripts are embedded within HTML and executed on the server, generating dynamic web pages.

### Master & Slave:
Master and Slave are terms that can be used to describe the relationship between different systems or components, particularly in the context of configuration and communication.     

### Ansible:
Ansible is an open-source automation and configuration management tool that simplifies and streamlines IT operations. It is designed to help system administrators and DevOps teams automate repetitive tasks, deploy applications, manage configurations, and orchestrate complex workflows on a wide range of servers and infrastructure environments. Here are the key aspects of Ansible:    

---
- [ ] **Explaining Different Section in this Repo**

### Ansible Playbook: 
- An Ansible playbook is a script written in YAML format that defines a set of tasks and configurations to be executed on target hosts. Playbooks are at the core of Ansible automation and serve as a way to automate and orchestrate various system administration and infrastructure tasks. Here's a brief explanation of key components and concepts related to Ansible playbooks:

### Ansible.cfg:
- The ansible.cfg file is a configuration file used by Ansible to customize its behavior and settings. It is typically located in the /etc/ansible/ directory or in the current directory where Ansible is executed. Here's a brief explanation of the ansible.cfg file:    
<img width="700" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/b979cd4f-6959-4fde-bab6-22008ec7c036">

- The ansible.cfg file is a valuable tool for tailoring Ansible's behavior to meet your specific automation needs. It provides flexibility, maintainability, and improved project organization by allowing you to define and document configuration settings at the project level.

### Ansible Inventory:
- The Ansible inventory file is a critical component that defines the hosts and groups of hosts on which Ansible will operate. It is essentially a list of target hosts that Ansible will connect to and manage. 
<img width="700" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/61e9e66b-7611-43c8-b2bb-5ba42182d988">

- It provides a structured way to organize hosts, group them logically, set variables, and create a dynamic view of your environment. This flexibility makes Ansible well-suited for a wide range of automation tasks across various types of infrastructures.

### Site.yml file:

- **Update the server repos**:
It uses the ansible.builtin.apt module to update the package repositories and upgrade the installed packages on the remote hosts.

**Cronjob to check uptime every 12 am**:

- It uses the ansible.builtin.cron module to set up a cron job that runs the /usr/bin/uptime command every day at midnight (12 a.m.) and redirects the output to a log file.

**Copy the script to slave nodes**:

- It uses the ansible.builtin.copy module to copy a script file named "bash-slave.sh" to the remote hosts in the home directory (~/) with specific ownership and permissions.

**Change permission on script**: 
- It uses the ansible.builtin.command module to change the permissions of the "bash-slave.sh" script file, making it executable.

**Execute a command**: 
- This task uses the ansible.builtin.command module to execute the "bash-slave.sh" script with specific arguments (michael and michael19). The < /dev/null part is 

### Stack.sh file
- This script appears to automate the setup of a LAMP (Linux, Apache, MySQL, PHP) stack environment and deploy a Laravel application on a Ubuntu server. Let's break down its main components and actions:

1. **Server Repository Update:** It starts by updating the package repository and upgrading installed packages on the server using `apt`.

2. **LAMP Stack Installation:**
   - Apache (`apache2`) is installed.
   - MySQL Server (`mysql-server`) is installed.
   - A third-party PHP repository is added (`ppa:ondrej/php`) and PHP and its necessary modules are installed.
   - PHP configuration changes are made to disable `cgi.fix_pathinfo` for security reasons.
   - The Apache service is restarted to apply changes.

3. **Composer Installation:** It installs Composer, a PHP dependency manager.

4. **Apache Configuration:** It creates an Apache virtual host configuration file for Laravel in `/etc/apache2/sites-available/laravel.conf`. This configuration sets up the document root for the Laravel application and allows URL rewriting.

5. **Apache Modules:** It enables the Apache `rewrite` module and enables the newly created Laravel site.

6. **Laravel Installation:** It creates a directory for the Laravel application, clones the Laravel repository from GitHub and runs `composer install` to install the application's PHP dependencies.

7. **File Permissions:** It sets file and directory permissions for the Laravel application, making sure the web server user (`www-data`) has the appropriate access.

8. **Database Setup:** It creates a MySQL database, a MySQL user, and grants the user privileges on the database. It generates a random password if none is provided.

9. **Laravel Configuration:** It updates the Laravel application's `.env` file to configure the database connection parameters.

10. **Caching and Migration:** It runs commands to cache the Laravel configuration and perform database migrations.

### Master-slave file:
This script creates two Ubuntu-based virtual machines, "Moscow" and "Germany," configures private network IP addresses, and provisions them with specific packages using shell scripts. It's a basic setup for a Vagrant development environment with two VMs.

1. `vagrant init ubuntu/focal64`: Initializes a new Vagrant project and sets the base box to "ubuntu/focal64."

2. The script uses a "here document" (the `cat <<EOF >>Vagrantfile` block) to generate a Vagrant configuration within a `Vagrantfile`. The Vagrant configuration is defined in Ruby DSL format.

3. Inside the `Vagrant.configure` block, it defines two virtual machines: "Moscow" and "Germany."

   - For the "Moscow" VM:
     - Sets the hostname to "Moscow."
     - Uses the "ubuntu/focal64" base box.
     - Configures a private network with a static IP address of "192.168.56.11."
     - Specifies provisioning using a shell script. This script updates the system and installs "avahi-daemon" and "libnss-mdns."

   - For the "Germany" VM:
     - Sets the hostname to "Germany."
     - Uses the same "ubuntu/focal64" base box.
     - Configures a private network with a static IP address of "192.168.56.10."
     - Specifies provisioning using a similar shell script for updating and installing "avahi-daemon" and "libnss-mdns."

4. Lastly, it configures the provider-specific settings for VirtualBox, allocating 1024 MB of memory and 2 CPUs to each VM.

5. The `vagrant up` command is executed to create and provision the VMs based on the configurations defined in the `Vagrantfile`. This command launches the virtual machines using the specified settings.

---

- [ ] How To Run The Repo

The Tools Needed To Run This:
  - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  - [Vagrant](https://developer.hashicorp.com/vagrant/downloads)

  - Create a directory for the project

  Inside the directory create a script file `master-slave.sh`, this script will spins up the creation of both master and slave machine. then another stacks.sh this script provisions the installation of lamp stack on the master node and deploys laravel on the master node

- Inside the directory create a sub-folder ‘ansible-playbook’ inside the ansible-playbook create the following files: ansible.cfg, inventory, onsite.yml



- Open a Terminal: Open a terminal on your Ubuntu system.
- Make the Script Executable: If the script is not already marked as executable, you need to do so. Navigate to the directory where your script is located and run the following command:
- Make some modifications to the `.env`:
  - In the .env change the USERNAME, DATABASE, and PASSWORD
  - Modify Mysql
  - change the ServerName to your IP address
  - modify the ansible config file
  - on your terminal run the script with the argument `./stacks.sh michael michael19`








---

## [REQUIREMENTS]()

### Ansible Playbook:   
The Ansible playbook consists of the configuration-file, Inventory, and the onsite-play
- Ansible configuration file
  ``` yaml
   [defaults]
  inventory = inventory
  private_key_file = ~/.ssh/id_rsa
  host_key_checking = false
  ```

- Ansible Inventory
  ``` plaintext
   192.168.56.11
  ```
- Ansible play

   ``` yaml
	    ---
	- name: Transferring Files to the slave node
	  hosts: all
	  become: true
	  pre_tasks:
	    - name: Update the server repos
	      ansible.builtin.apt:
	        update_cache: yes
	        upgrade: yes
	
	    - name: Cronjob to check uptime every 12 am
	      ansible.builtin.cron:
	        name: Cronjob uptime every 12 am
	        minute: "0"
	        hour: "0"
	        day: "*"
	        month: "*"
	        weekday: "*"
	        job: "/usr/bin/uptime > /var/log/uptime_check.log 2>&1"
	        state: present
	
	    - name: Copy the script to slave nodes
	      ansible.builtin.copy:
	        src: stacks.sh
	        dest: ~/
	        owner: root
	        group: root
	        mode: "0744"
	
	    - name: Change permission on script
	      command: chmod +x ~/stacks.sh
	
	    - name: Execute a command
	      command: bash stacks.sh michael michael19 < /dev/null

  ```

- Provisioning Sript For LAMP Stack and Other Dependencies

  ``` bash
  
	#!/bin/bash
	
	# UPDATING & UPGRADING THE SERVER
	#################################
	
	sudo apt update && sudo apt upgrade -y </dev/null
	
	# INSTALLATION OF LAMP STACK
	#############################
	
	sudo apt-get install apache2 -y </dev/null
	
	sudo apt-get install mysql-server -y </dev/null
	
	sudo add-apt-repository -y ppa:ondrej/php </dev/null
	
	sudo apt-get update </dev/null
	
	sudo apt-get install libapache2-mod-php php php-common php-xml php-mysql php-gd php-mbstring php-tokenizer php-json php-bcmath php-curl php-zip unzip -y </dev/null
	
	sudo sed -i 's/cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php/8.2/apache2/php.ini
	
	sudo systemctl restart apache2 </dev/null
	
	# INSTALLING COMPOSER
	###################
	
	sudo apt install curl -y
	
	sudo curl -sS https://getcomposer.org/installer | php
	
	sudo mv composer.phar /usr/local/bin/composer
	
	composer --version </dev/null
	
	# SETTING UP APACHE2
	###########################
	
	cat <<EOF >/etc/apache2/sites-available/laravel.conf
	<VirtualHost *:80>
	    ServerAdmin mykaelgeorge@gmail.com
	    ServerName 192.168.56.10
	    DocumentRoot /var/www/html/laravel/public
	
	    <Directory /var/www/html/laravel>
	    Options Indexes MultiViews FollowSymLinks
	    AllowOverride All
	    Require all granted
	    </Directory>
	
	    ErrorLog ${APACHE_LOG_DIR}/error.log
	    CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>
	EOF
	
	sudo a2enmod rewrite
	
	sudo a2ensite laravel.conf
	
	sudo systemctl restart apache2
	
	# CLONE LARAVEL APPLICATION AND DEPENDENCIES
	############################################
	
	mkdir /var/www/html/laravel && cd /var/www/html/laravel
	
	cd /var/www/html && sudo git clone https://github.com/laravel/laravel.git
	
	cd /var/www/html/laravel && composer install --no-dev </dev/null
	
	sudo chown -R www-data:www-data /var/www/html/laravel
	
	sudo chmod -R 775 /var/www/html/laravel
	
	sudo chmod -R 775 /var/www/html/laravel/storage
	
	sudo chmod -R 775 /var/www/html/laravel/bootstrap/cache
	
	cd /var/www/html/laravel && sudo cp .env.example .env
	
	php artisan key:generate
	
	# CONFIGURING MYSQL: CREATING USER AND PASSWORD
	###############################################
	
	echo "Creating MySQL user and database"
	PASS=$2
	if [ -z "$2" ]; then
	  PASS=$(openssl rand -base64 8)
	fi
	
	mysql -u root <<MYSQL_SCRIPT
	CREATE DATABASE $1;
	CREATE USER '$1'@'localhost' IDENTIFIED BY '$PASS';
	GRANT ALL PRIVILEGES ON $1.* TO '$1'@'localhost';
	FLUSH PRIVILEGES;
	MYSQL_SCRIPT
	
	echo "MySQL user and database created."
	echo "Username:   $1"
	echo "Database:   $1"
	echo "Password:   $PASS"
	
	# EXECUTE KEY GENERATE AND MIGRATE COMMAND FOR PHP
	##################################################
	
	sudo sed -i 's/DB_DATABASE=laravel/DB_DATABASE=michael/' /var/www/html/laravel/.env
	
	sudo sed -i 's/DB_USERNAME=root/DB_USERNAME=michael/' /var/www/html/laravel/.env
	
	sudo sed -i 's/DB_PASSWORD=/DB_PASSWORD=michael19/' /var/www/html/laravel/.env
	
	php artisan config:cache
	
	cd /var/www/html/laravel && php artisan migrate
  ```

- Provisioning The VM'S

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
	    SHELL
	  end
	
	    config.vm.provider "virtualbox" do |vb|
	      vb.memory = "1024"
	      vb.cpus = "2"
	    end
	end
	EOF
	
	vagrant up

  ```

- Laravel Homepage

  - The Master Node: 192.168.56.10
<img width="700" alt="Screenshot 2023-10-22 at 9 58 53 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/d723649b-1831-4e16-b1ee-b6329afdd233">

  - The Slave Node: 192.168.56.11
<img width="700" alt="Screenshot 2023-10-23 at 4 58 48 AM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/3a0523af-4197-43ce-9487-2a6a4c1c2bf0">

- MySQL Data
<img width="700" alt="Screenshot 2023-10-22 at 10 01 26 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/d631025a-aa47-47d4-bb11-484a768eed43">








