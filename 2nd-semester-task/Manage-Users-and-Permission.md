# AltSchool Cloud-Engineering Assignment

## [Assignment]() 1
### Task: 
* Setup Ubuntu 20.04 LTS on your local machine using Vagrant
### Instruction: 
- create a user
- set an expiry date of 2weeks for the user
- prompt the user to change there password on login
- attach the user to a group called altschool
- allow altschool group to be able to run only cat command on /etc/
- create another user. make sure that this user doesn't have a home directory.
---

[Solution] 1

 **Create a User with Expiry Date:**
   
   You can use the `useradd` command to create a new user
   ```
   sudo useradd george
   ```
 **Set an expiry date of 2 weeks for the user**
   run the command below to set an `expiry date`
```
 sudo chage -E $(date -d "+2 weeks" +"%Y-%m-%d") george
```

 **Prompt User to Change Password on Login:**

  you can use the `passwd` command to enforce a password change on the next login:

   ```
   sudo passwd -e george
   ```

**Attach User to a Group:**
- first off you'll need to create the intended group, to do that;
- run the command below

```
sudo groupadd Altschool
```
  
  You can use the `usermod` command to add the user to a group.
  ```
   sudo usermod -aG Altschool george
  ```

**Allow Group to Run Only `cat` Command on `/etc/`:**

   To restrict a group to only run the `cat` command on the `/etc/` directory, you can use the `sudoers` configuration file (`/etc/sudoers`). Edit the file using the `visudo` command (always use `visudo` to edit sudoers file):

   ```bash
   sudo visudo
   ```






