# Testing-Linux-and-Servers

This repository contains the implementation for setting up a secure, monitored, and well-maintained development environment for new developers Sarah and Mike. The tasks include system monitoring, user management, and automated backup configuration.

---

## Table of Contents

1. [Task 1: System Monitoring Setup](#task-1-system-monitoring-setup)
2. [Task 2: User Management and Access Control](#task-2-user-management-and-access-control)
3. [Task 3: Backup Configuration for Web Servers](#task-3-backup-configuration-for-web-servers)
4. [Report and Challenges](#report-and-challenges)
5. [Submission](#submission)

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
![image](https://github.com/user-attachments/assets/54921845-194d-418f-8c79-62b15295bd4c)
![image](https://github.com/user-attachments/assets/bb92cb93-f734-414f-90ab-c4fefa2a76e6)
![image](https://github.com/user-attachments/assets/57dc9c50-7b42-49dc-ace2-74ffd8fba16c)

- Example log file: `monitoring.log`
![image](https://github.com/user-attachments/assets/a9f7768d-98d4-4eb1-b699-b2818a8d9726)
![image](https://github.com/user-attachments/assets/db42fb32-4cee-491a-9df3-fc260dd96a50)



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
![image](https://github.com/user-attachments/assets/135ac087-a267-4a49-9303-8cf0d4ac018f)
![image](https://github.com/user-attachments/assets/2838bccf-909c-4a9c-bbaf-47877924f504)

- Documentation of password policy enforcement.
![image](https://github.com/user-attachments/assets/f4b7ab55-fc16-4a86-a321-7ccea1d83f3b)

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
![image](https://github.com/user-attachments/assets/eca1d81c-786f-4cb3-aedf-1da9c78074a2)
![image](https://github.com/user-attachments/assets/8cdc5c75-e511-4739-ac90-3017af813929)


- Verification logs showing successful backup contents.
![image](https://github.com/user-attachments/assets/89b3d1c9-bcd9-40a0-874f-1660e39f56d1)
![image](https://github.com/user-attachments/assets/24593261-da65-47ad-9248-f715eb6254e6)

---

@@ -204,7 +206,7 @@

## Submission

The full implementation and supporting files are available in this repository. Access the project at: [GitHub Repository Link](#).
The full implementation and supporting files are available in this repository. Access the project at: [[GitHub Repository Link](https://github.com/aakashrawat1910/Testing-Linux-and-Servers.git)](#).

