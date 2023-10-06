# AltSchool Cloud-Engineering Exercises

## [Exercise] 1
### Task: 
* Setup Ubuntu 20.04 LTS on your local machine using Vagrant
### Instruction: 
- Customize your Vagrant file as necessary with private_network set to DHCP.
- Once the machine is up, run ifconfig and share the output in your submission along with your Vagrant file in a folder for this exercise.
---

 ### [Solution] 1

 To set up Ubuntu 20.04 LTS on your local machine using Vagrant with a private network set to DHCP, follow these steps:

 **Create a New Directory:**

 - Create a new directory where you'll store your Vagrant configuration files.

   ```
   mkdir ubuntu-20.04-vagrant
   cd ubuntu-20.04-vagrant
   ```

 **Initialize Vagrant:**

 - Initialize a new Vagrant environment in the directory you just created.

   ```bash
   vagrant init ubuntu/focal64
   ```
 - Below is the Vagrantfile
``` ruby
     # -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    config.vm.network "private_network", type: "dhcp"
  
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/focal64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessable to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-END
    apt-get update
    apt-get install -y apache2
    cp -r /vagrant/webcontent/* /var/www/html/
    echo "Machine provisioned at $(date)! Welcome!"
  END
end
```
   **Start and Provision the Virtual Machine:**

 - Start the virtual machine and provision it with Ubuntu 20.04 LTS.

   ```
   vagrant up
   ```

 **SSH into the Virtual Machine:**

 - Once the virtual machine is up and running, you can SSH into it.

   ```
   vagrant ssh
   ```
 **Check Network Configuration:**

 - Inside the virtual machine, run `ifconfig` to check the network configuration:

   ```
   ifconfig
   ```
<img width="700" alt="Screenshot 2023-10-06 at 12 33 46 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/ebb81853-e005-4ae8-90f7-b0db558d626c">
