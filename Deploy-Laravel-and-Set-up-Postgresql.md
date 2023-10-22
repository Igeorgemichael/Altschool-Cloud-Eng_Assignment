## [Exam Project]()
### Task

---
## [Solution]()

what this repo is all about   
Laravel: Laravel is a popular open-source PHP web application framework known for its elegant syntax, developer-friendly features, and robust set of tools for building modern web applications. It was created by Taylor Otwell and first released in 2011. Laravel follows the Model-View-Controller (MVC) architectural pattern and provides a range of features to simplify and speed up web development.
- Some key features
  - Eloquent ORM
  - Artisan Console
  - Blade Templating Engine
  - Authentication and Authorization
  - Routing
  - Database Migrations and Seeding
  - Testing

A LAMP stack is a popular open-source web development platform that consists of four key components, each of which plays a specific role in web application development. The term "LAMP" is an acronym that represents these four components:

- Linux: Linux is the operating system that forms the foundation of the LAMP stack. It provides the environment for hosting web applications and serves as the server's underlying operating system. Linux is chosen for its stability, security, and versatility. Popular Linux distributions used in LAMP stacks include Ubuntu, CentOS, and Debian.
- Apache: Apache is the web server software in the LAMP stack. It's responsible for handling client requests and serving web content to users' web browsers. Apache is highly configurable and supports a wide range of web-related technologies. It's known for its reliability and widespread use in the web hosting industry.
- MySQL (or MariaDB): MySQL is the relational database management system (RDBMS) used in the LAMP stack for storing and managing data. It is known for its speed and reliability, making it a popular choice for web applications. MariaDB, a fork of MySQL, is often used as an alternative due to its open-source nature and enhanced performance.
- PHP: PHP is the server-side scripting language that enables the dynamic generation of web content and interactions with the database. It's a powerful language for web development and is widely used for creating web applications. PHP scripts are embedded within HTML and executed on the server, generating dynamic web pages.


"master" and "slave" are terms that can be used to describe the relationship between different systems or components, particularly in the context of configuration and communication.     

Ansible is an open-source automation and configuration management tool that simplifies and streamlines IT operations. It is designed to help system administrators and DevOps teams automate repetitive tasks, deploy applications, manage configurations, and orchestrate complex workflows on a wide range of servers and infrastructure environments. Here are the key aspects of Ansible:    

---
## Explaining Different Section in this Repo
**Ansible Playbook**: 
An Ansible playbook is a script written in YAML format that defines a set of tasks and configurations to be executed on target hosts. Playbooks are at the core of Ansible automation and serve as a way to automate and orchestrate various system administration and infrastructure tasks. Here's a brief explanation of key components and concepts related to Ansible playbooks:

## Ansible.cfg:
The ansible.cfg file is a configuration file used by Ansible to customize its behavior and settings. It is typically located in the /etc/ansible/ directory or in the current directory where Ansible is executed. Here's a brief explanation of the ansible.cfg file:    

The ansible.cfg file is a valuable tool for tailoring Ansible's behavior to meet your specific automation needs. It provides flexibility, maintainability, and improved project organization by allowing you to define and document configuration settings at the project level.

## Ansible Inventory:
The Ansible inventory file is a critical component that defines the hosts and groups of hosts on which Ansible will operate. It is essentially a list of target hosts that Ansible will connect to and manage. 

The Ansible inventory file is a central component that defines the infrastructure Ansible will manage. It provides a structured way to organize hosts, group them logically, set variables, and create a dynamic view of your environment. This flexibility makes Ansible well-suited for a wide range of automation tasks across various types of infrastructures.

## Site.yml file:
- this file holds the cronjob
- this file also makek provisioninig for copying file from one node to another
- this changes the command of the file
- this also runs the stack.sh script that is available

## Stack.sh file
This script appears to automate the setup of a LAMP (Linux, Apache, MySQL, PHP) stack environment and deploy a Laravel application on a Ubuntu server. Let's break down its main components and actions:

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

6. **Laravel Installation:** It creates a directory for the Laravel application, clones the Laravel repository from GitHub, and runs `composer install` to install the application's PHP dependencies.

7. **File Permissions:** It sets file and directory permissions for the Laravel application, making sure the web server user (`www-data`) has appropriate access.

8. **Database Setup:** It creates a MySQL database, a MySQL user, and grants the user privileges on the database. It generates a random password if none is provided.

9. **Laravel Configuration:** It updates the Laravel application's `.env` file to configure the database connection parameters.

10. **Caching and Migration:** It runs commands to cache the Laravel configuration and perform database migrations.

## Master-slave file:
This script creates two Ubuntu-based virtual machines, "moscow" and "germany," configures private network IP addresses, and provisions them with specific packages using shell scripts. It's a basic setup for a Vagrant development environment with two VMs.

1. `vagrant init ubuntu/focal64`: Initializes a new Vagrant project and sets the base box to "ubuntu/focal64."

2. The script uses a "here document" (the `cat <<EOF >>Vagrantfile` block) to generate a Vagrant configuration within a `Vagrantfile`. The Vagrant configuration is defined in Ruby DSL format.

3. Inside the `Vagrant.configure` block, it defines two virtual machines: "moscow" and "germany."

   - For the "moscow" VM:
     - Sets the hostname to "moscow."
     - Uses the "ubuntu/focal64" base box.
     - Configures a private network with a static IP address of "192.168.56.11."
     - Specifies provisioning using a shell script. This script updates the system and installs "avahi-daemon" and "libnss-mdns."

   - For the "germany" VM:
     - Sets the hostname to "germany."
     - Uses the same "ubuntu/focal64" base box.
     - Configures a private network with a static IP address of "192.168.56.10."
     - Specifies provisioning using a similar shell script for updating and installing "avahi-daemon" and "libnss-mdns."

4. Lastly, it configures the provider-specific settings for VirtualBox, allocating 1024 MB of memory and 2 CPUs to each VM.

5. The `vagrant up` command is executed to create and provision the VMs based on the configurations defined in the `Vagrantfile`. This command launches the virtual machines using the specified settings.










