## [Exercise] 4
### Task: 
* Install PHP 7.4 on your local linux machine using the ppa:ondrej/php package repo.
### Instruction:
- Learn how to use the add-apt-repository command
- Submit the content of /etc/apt/sources.list and the output of php -v command
---

 ### [Solution] 4

To install PHP 7.4 on your local Linux machine using the `ppa:ondrej/php` package repository, 
**Add the `ppa:ondrej/php` Repository:**

- The `add-apt-repository` command is used to add external repositories.
   ```
   sudo apt-get update
   sudo apt-get install software-properties-common
   ```

- This command below adds the repository to your system.

  After installing `software-properties-common`,
  
  you can use `add-apt-repository`
  
  add the `ppa:ondrej/php` repository:

   ```
   sudo add-apt-repository ppa:ondrej/php
   ```

**Update the Package List:**

- Update the package list to include the new repository:
   
  run: `sudo apt-get update`

**Install PHP 7.4:**

- Now that the repository is added and the package list is updated, you can install PHP 7.4:

   ```
   sudo apt-get install php7.4
   ```
**Submit Required Contents:**
- cat /etc/apt/sources.list
<img width="700" alt="Screenshot 2023-10-06 at 4 20 44 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/9e296896-a05e-48be-949c-836b280f1af2">

- php -v 
<img width="700" alt="Screenshot 2023-10-06 at 4 22 55 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/cbfb60ef-f38e-46f6-8c14-8ded1aad7e37">








