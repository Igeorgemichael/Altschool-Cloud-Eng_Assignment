## [Exercise]() 3
### Task:
* Create 3 groups – admin, support & engineering and add the admin group to sudoers. 
* Create a user in each of the groups. 
* Generate SSH keys for the user in the admin group.
### Instruction:
- [ ] Submit the contents of /etc/passwd, /etc/group, /etc/sudoers
---
 ## [Solution]() 3

 **Create Groups and Add Admin Group to sudoers:**

   Create the three groups - `admin`, `support`, and `engineering`, and add the `admin` group to the sudoers file to grant sudo privileges.

   ```
   # Create groups
   sudo groupadd admin
   sudo groupadd support
   sudo groupadd engineering

   # Add the admin group to sudoers
   sudo visudo
   ```
Inside the sudoers file, add the following line to grant sudo privileges to the `admin` group:

   ```
   %admin ALL=(ALL:ALL) ALL
   ```

   Save and exit the sudoers file.
<img width="600" alt="Screenshot 2023-10-06 at 2 57 09 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/875f68cd-939f-430e-9417-a30cb1e4aa4b">

Create a user in each of the three groups - `adminuser`, `supportuser`, and `engineeruser`.

   ```
   # Create users and assign them to groups
   sudo useradd -m -G admin adminuser
   sudo useradd -m -G support supportuser
   sudo useradd -m -G engineering engineeruser
   ```

   Set passwords for the newly created users:

   ```
   sudo passwd adminuser
   sudo passwd supportuser
   sudo passwd engineeruser
   ```

 **Generate SSH Keys for the Admin User:**

   Generate SSH keys for the `adminuser` in the `admin` group.
<img width="600" alt="Screenshot 2023-10-06 at 3 48 56 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/b8a3af0e-c091-4c7a-893b-8976b414812f">

 **Submit Contents of Required Files:**
 
   - sudo cat /etc/passwd
<img width="600" alt="Screenshot 2023-10-06 at 3 43 16 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/f112f4d7-3691-4141-8f40-bdbd2865cd92">

   - sudo cat /etc/group
<img width="600" alt="Screenshot 2023-10-06 at 3 45 54 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/3232eac2-06c5-41dc-95cd-3c1889654168">

   - sudo cat /etc/sudoers
<img width="600" alt="Screenshot 2023-10-06 at 4 06 30 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/5301bb4b-34ca-4baa-8506-bd8be4b6ca3c">




