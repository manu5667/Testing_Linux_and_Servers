# Testing-Linux-and-Servers

This repository contains the implementation for setting up a secure, monitored, and well-maintained development environment for new developers Sarah and Mike. The tasks include system monitoring, user management, and automated backup configuration.

---

## Table of Contents

1. [Task 1: System Monitoring Setup](#task-1-system-monitoring-setup)
2. [Task 2: User Management and Access Control](#task-2-user-management-and-access-control)
3. [Task 3: Backup Configuration for Web Servers](#task-3-backup-configuration-for-web-servers)
4. [Report and Challenges](#report-and-challenges)


---

## Task 1: System Monitoring Setup

### Objective
Configure a monitoring system to ensure the health, performance, and capacity planning of the development environment.

### Steps
1. **Installed monitoring tools:**
    - Install `htop`:
      ```bash
      sudo apt update
      sudo apt install htop -y
      ```
    - Install `nmon`:
      ```bash
      sudo apt update
      sudo apt install nmon -y
      ```
2. **Configured disk usage monitoring:**
    - Use `df` for overall disk space monitoring:
      ```bash
      df -h
      ```
    - Use `du` for directory-level disk usage analysis:
      ```bash
      du -sh /path/to/directory
      ```
      - Create a script to log disk usage periodically:
      ```bash
      #!/bin/bash
      df -h > /var/log/disk_usage_$(date +%F).log
      du -sh /path/to/directory >> /var/log/disk_usage_$(date +%F).log
      ```
      Add to cron for daily execution:
      ```bash
      crontab -e
      0 0 * * * /path/to/disk_usage_monitor.sh
      ```
      3. **Implemented process monitoring:**
    - Identify resource-intensive processes using `htop`:
      ```bash
      htop
      ```
    - Use `ps aux` for detailed process information:
      ```bash
      ps aux --sort=-%mem
      ```
        - Create a script to log top 10 resource-intensive processes:
      ```bash
      #!/bin/bash
      ps aux --sort=-%mem | head -n 10 > /var/log/process_monitor_$(date +%F).log
      ```
      Add to cron for hourly execution:
      ```bash
      crontab -e
      0 * * * * /path/to/process_monitor.sh
      ```
      4. **Set up logging:**
    - Save monitoring outputs to `/var/logs/monitoring.log` using scheduled scripts:
      ```bash
      htop -b -n 1 > /var/logs/monitoring.log
      ```
      ### Outputs
- Screenshots of `htop`, `nmon`, and disk usage commands.
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/560968b1e426b72140691c3c7e1f4c4f6b71f36f/s1.png)
   ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/560968b1e426b72140691c3c7e1f4c4f6b71f36f/s2.png)
   ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/560968b1e426b72140691c3c7e1f4c4f6b71f36f/s3.png)
- Example log file: `monitoring.log`
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/560968b1e426b72140691c3c7e1f4c4f6b71f36f/s4.png)
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/560968b1e426b72140691c3c7e1f4c4f6b71f36f/s5.png)
      
      
  ## Task 2: User Management and Access Control

### Objective
Create user accounts and configure secure access controls for Sarah and Mike.

### Steps
1. **Created user accounts:**
    - Add Sarah:
      ```bash
        sudo adduser sarah
       ```
    - Add Mike:
      ```bash
       sudo adduser mike
       ```
2. **Created dedicated directories:**
    - Create Sarah's workspace:
      ```bash
         sudo mkdir -p /home/sarah/workspace
        ```
    - Create Mike's workspace:
      ```bash
         sudo mkdir -p /home/mike/workspace
       ```
3. **Set permissions:**
    - Ensure only Sarah has access to her workspace:
      ```bash
      sudo chmod 700 /home/sarah/workspace
      sudo chown sarah:sarah /home/sarah/workspace
      ```
    - Ensure only Mike has access to his workspace:
      ```bash
      sudo chmod 700 /home/mike/workspace
      sudo chown mike:mike /home/mike/workspace
      ```
    4. **Enforced password policies:**
    - Configure password expiration every 30 days:
      ```bash
      sudo chage -M 30 sarah
      sudo chage -M 30 mike
      ```
      ### Outputs
- Screenshots of user creation and permission setups.
 ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s6.png)
 ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s7.png)

- Documentation of password policy enforcement.
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s8.png)

---

   ## Task 3: Backup Configuration for Web Servers

### Objective
Automate backups for Sarah's Apache server and Mike's Nginx server, ensuring data integrity and recovery.

### Steps
1. **Configured backup scripts:**
    - Sarah's Apache backup script:
      ```bash
      #!/bin/bash
      tar -czf ~/workspace/backup/apache_backup_$(date +%F).tar.gz /etc/apache2/ /var/www/html/
      ```
    - Mike's Nginx backup script:
      ```bash
      #!/bin/bash
      tar -czf ~/workspace/backup/nginx_backup_$(date +%F).tar.gz /etc/nginx/ /usr/share/nginx/html/
      ```
2. **Scheduled cron jobs:**
    - Sarah's backup cron job:
      ```bash
      crontab -e
      0 0 * * 2 /path/to/apache_backup.sh
      ```
    - Mike's backup cron job:
      ```bash
      crontab -e
      0 0 * * 2 /path/to/nginx_backup.sh
      ```
3. **Verified backup integrity:**
    - List contents of the compressed files:
      ```bash
      tar -tvf /backups/apache_backup_$(date +%F).tar.gz
      tar -tvf /backups/nginx_backup_$(date +%F).tar.gz
      ```
      

### Outputs
- Backup files in `/backups/` directory.
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s9.png)
  ![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s10.png)


- Verification logs showing successful backup contents.
![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s11.png)
![image](https://github.com/manu5667/Testing_Linux_and_Servers/blob/c6f6231700af3bbc61703d5d7a25db6d695ed10f/s12.png)

---

## Report and Challenges

### Summary
- Successfully installed and configured monitoring tools (`htop`, `nmon`).
- User accounts and secure directories set up for Sarah and Mike with enforced password policies.
- Automated backups configured for Apache and Nginx servers with verified integrity.
