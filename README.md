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
- 
