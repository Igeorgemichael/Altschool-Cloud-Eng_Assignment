# AltSchool Cloud-Engineering Assignment

## [Assignment]() 1
### Instruction: 
- Create a user
- Set an expiry date of 2weeks for the user
- Prompt the user to change there password on login
- Attach the user to a group called altschool
- Allow altschool group to be able to run only cat command on /etc/
- Create another user. make sure that this user doesn't have a home directory.
---

## [Solution]() 1

 **Create a User with Expiry Date:**
   
- Use the `sudo useradd` command to create a new user
    
   ```
   sudo useradd george
   ```
<img width="729" alt="261608821-4827bb38-69a8-4b98-9649-698789f68e05" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/756373f6-4876-4cb8-b475-f94a81905f57">

- run `cat /etc/passwd` to verify the user is been created

<img width="727" alt="261608868-e3761d8b-dfb8-482c-8e4d-abc111501ceb" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/05044292-6745-4bdf-b107-5bc349c2b844">

 **Set an expiry date of 2 weeks for the user**
 
- Setting a password expiration that prompt the user to change his/her password on next `login`

   run the command below to set an `expiry date`
   
   ```
   sudo chage -E $(date -d "+2 weeks" +"%Y-%m-%d") george
   ```
<img width="726" alt="261608891-07faa69a-c983-4bf7-9f66-d3f538d08dc4" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/c0489f04-3290-4b37-b226-fd2c9da50d57">


**Prompt User to Change Password on Login:**

- Use the `passwd` command to enforce a password change on the next login:

   ```
   sudo passwd -e george
   ```

   -  run the command `sudo chage -l george` to view the password information
  
<img width="726" alt="261608961-e08f576a-b32d-4623-9704-ba3354b47dc1" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/863d51b4-3224-4452-9986-9eb935e5c763">


**Attach User to a Group:**

- Before adding user to the group, first off you'll need to create the intended group, to do that;
- run the command below

    `sudo groupadd Altschool`
  
  You can use the `usermod` command to add the user to a group.
  
   ```
   sudo usermod -aG Altschool george
   ```
<img width="728" alt="261608984-95df5d63-8549-4d22-8d15-c771a539fc30" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/a6c8d41a-1323-4255-a677-3c78024092df">

-
<img width="723" alt="261609020-409f8d78-8d31-4c16-8cd3-0da24a15d649" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/e98485cc-067f-4038-9641-93c697da3eba">


**Allow Group to Run Only `cat` Command on `/etc/`:**

- In order to deny a group to only run the `cat` command on the `/etc/` directory, you will visit the `sudoers` configuration file located at (`/etc/sudoers`).
- you will need to edit the file using the `visudo`:

   `sudo visudo`

  Then add the line below to the members of the admin group in the sudoer configuration

   ```plaintext
   %altschool ALL=(ALL) /bin/cat /etc/*
   ```
<img width="726" alt="261609057-6949ad15-87bc-4f86-b916-34e6523f9edf" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/c8577781-8a5d-4c3a-836a-f8faeba099c2">


**Create a User Without a Home Directory:**

- Use the `useradd` command with the `-M` option to create a user without a home directory. 
   
   `sudo useradd -M bryan`
<img width="728" alt="261609126-346a39f0-64b9-4da6-b7de-ac5d8ca713b9" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/dca32b07-c19c-4dee-b0f1-e13623fd1cd3">

-

<img width="730" alt="261609221-1e36c4ac-4405-4113-ba75-64ded117c696" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/f87de35a-d01b-4c96-860b-1109d967efa7">




