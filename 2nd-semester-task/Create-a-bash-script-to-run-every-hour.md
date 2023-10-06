## [Exercise]() 6

### Task:

* Create a bash script to run hourly, saving system memory (RAM) usage to a specified file and at midnight it sends the content of the file to a specified email address, then starts over for the new day.

### Instruction:

- Submit the content of your script, cronjob and a sample of the email sent, all in the folder for this exercise.
---
 ### [Solution]() 6

 **Create the Bash Script:**

- Create a new bash script, e.g., `memory_monitor.sh`, and make it executable:

   ```
   touch cronmemory.sh
   chmod +x cronmemory.sh
   ```

- Edit the script using a text editor like or `vim`:

   ```
   vim cronmemory.sh
   ```
- below is the script `memory_monitor.sh`
  
``` bash
#!/bin/bash

# Specify the file to save memory usage data
data_file="/home/michael/cronjob-task/memory_usage.txt"

# Get current date and time
timestamp=$(date +"%Y-%m-%d %H:%M:%S")

# Get memory usage and append it to the data file
memory_usage=$(free -m | awk 'NR==2{printf "Total: %s MB | Used: %s MB | Free: %s MB", $2, $3, $4}')
echo "$timestamp $memory_usage" >> "$data_file"

# Check if it's midnight (00:00)
if [[ $(date +"%H:%M") == "00:00" ]]; then
            # Send the contents of the data file via email
                cat "$data_file" | mail -s "Memory Usage Report" mykaelgeorge@gmail.com
                    # Clear the data file for a new day
                        > "$data_file"
fi
```

- In order to run the script every hour, Open your crontab job and edit:

   ```
   crontab -e
   ```

- Add the following line to schedule the script:

   ```
   0 * * * * /home/michael/cronjob-tasks/cronmemory.sh
   ```
<img width="508" alt="Screenshot 2023-10-06 at 9 48 56 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/95716602-699c-4686-a8b4-9440bbb578d7">

- A file named `memory_usage.txt`
  
<img width="508" alt="Screenshot 2023-10-06 at 9 44 01 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/78b634cd-3aca-433e-bf6e-b4260816debd">

- The Email sent
<img width="508" alt="Screenshot 2023-10-06 at 10 15 56 PM" src="https://github.com/Igeorgemichael/Altschool-Cloud-Eng_Assignment/assets/125099848/40187cf8-9008-43de-a643-86a3854c6229">


















