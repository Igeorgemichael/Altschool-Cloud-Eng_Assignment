### Task:
* Create an Ansible Playbook to setup a server with Apache
* The server should be set to the Africa/Lagos Timezone
* Host an index.php file with the following content, as the main file on the server:
```php
<?php
date_default_timezone_set('Africa/Lagos');
echo date("F d, Y h:i:s A e", time());
?>
```

### Instruction:
- Submit the Ansible playbook, the output of `systemctl status apache2` after deploying the playbook and a screenshot of the rendered page
---

## [Solution] 8

To set up a server with Apache, configure the Africa/Lagos timezone, and host an index.php file with the specified content,

 **Create the Ansible Playbook:**

   `apache-timezone.yml`:
   
``` yaml
---

- name: Set up Apache Server
  hosts: michael@192.168.65.2
  become: yes

  tasks:

    - name: update repository index for Ubuntu
      apt:
        update_cache: yes
      when: ansible_distribution_version == "Ubuntu"

    - name: Installing Apache
      apt:
        name: apache2
      notify:
        - Start Apache

    - name: Configure Timezone to Africa/Lagos
      timezone:
        name: Africa/Lagos

    - name: Create index.php file
      copy:
        content: |
          <?php
          echo date("F d, Y h:i:s A e", time());
        dest: /var/www/html/index.php
      notify:
        - Restart Apache

  handlers:
    - name: Start Apache
      service:
        name: apache2
        state: started
        enabled: yes

    - name: Restart Apache
      service:
        name: apache2
        state: restarted
```

**Run the Ansible Playbook:**

 - Run the playbook using the `ansible-playbook` command:

   ``` bash
   ansible-playbook --ask-become-pass apache-timezone.yml
   ```
<img width="700" alt="Screenshot 2023-10-06 at 11 53 26 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/5c97aef4-eede-49bd-aed7-2a8bc5fc44d6">

**Verify Apache Status:**

- run the command below to verify the Apache status
   
   ```bash
   systemctl status apache2
   ```
<img width="700" alt="Screenshot 2023-10-06 at 11 55 49 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/a68a271e-678c-45d8-9b52-a73f38349266">

**Verify the Rendered Page:**
- run the command below to display the output
  ```bash
   curl http://your_server_ip/index.php
   ```
<img width="700" alt="Screenshot 2023-10-07 at 12 52 31 AM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/c339bd41-4143-4790-9ff8-18a8d86421ef">

