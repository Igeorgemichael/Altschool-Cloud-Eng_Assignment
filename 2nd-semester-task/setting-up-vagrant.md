# AltSchool Cloud-Engineering Exercises

## [Exercise]() 1
### Task: 
* Setup Ubuntu 20.04 LTS on your local machine using Vagrant
### Instruction: 
- [ ] Customize your Vagrant file as necessary with private_network set to DHCP.
- [ ] Once the machine is up, run ifconfig and share the output in your submission along with your Vagrant file in a folder for this exercise.
---

 ### [Solution]()

 To set up Ubuntu 20.04 LTS on your local machine using Vagrant with a private network set to DHCP, follow these steps:

 **Create a New Directory:**

   Create a new directory where you'll store your Vagrant configuration files.

   ```
   mkdir ubuntu-20.04-vagrant
   cd ubuntu-20.04-vagrant
   ```

 **Initialize Vagrant:**

   Initialize a new Vagrant environment in the directory you just created.

   ```bash
   vagrant init ubuntu/focal64
   ```

 **Start and Provision the Virtual Machine:**

   Start the virtual machine and provision it with Ubuntu 20.04 LTS.

   ```
   vagrant up
   ```

 **SSH into the Virtual Machine:**

   Once the virtual machine is up and running, you can SSH into it.

   ```
   vagrant ssh
   ```
 **Check Network Configuration:**

   Inside the virtual machine, run `ifconfig` to check the network configuration:

   ```
   ifconfig
   ```
<img width="917" alt="Screenshot 2023-10-06 at 12 33 46 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/ebb81853-e005-4ae8-90f7-b0db558d626c">
