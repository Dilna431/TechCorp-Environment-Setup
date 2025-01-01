# Development Environment Setup for New Developers

This repository focuses on setting up a secure, monitored, and well-maintained development environment for new developers, Sarah and Mike. The setup includes tasks such as configuring system monitoring, managing user accounts and access control, and automating backup procedures for their web servers.

---

## Task 1: System Monitoring Setup

### Objective:
To ensure the development environment’s health, performance, and capacity planning.

### Steps:

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
     htop -b -n 1 > /var/log/system_metrics.log
     df -h >> /var/log/system_metrics.log
     du -sh /home >> /var/log/system_metrics.log
     ```

   - Add to cron for daily execution:
     ```bash
     crontab -e
     0 0 * * * /path/to/monitoring_script.sh
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

   - Add to cron for hourly execution:
     ```bash
     crontab -e
     0 * * * * /path/to/process_monitor.sh
     ```

4. **Set up logging:**

   - Save monitoring outputs to `/var/logs/monitoring.log` using scheduled scripts:
     ```bash
     htop -b -n 1 > /var/logs/monitoring.log
     ```

### Outputs:

- Screenshots of `htop`, `nmon`, and disk usage commands
- ![image](https://github.com/user-attachments/assets/92a633bb-365a-46fb-9c70-8735cdcb8aeb)
- 
- ![image](https://github.com/user-attachments/assets/19bfc481-399f-4be2-8639-654bac1fbb22)
- 
- ![image](https://github.com/user-attachments/assets/819968e7-67e7-4609-afa4-a98c276d9193)
- 
- ![image](https://github.com/user-attachments/assets/0e2c2caa-9bcf-4f09-bbe9-2c6aef730d0a)
- 
- ![image](https://github.com/user-attachments/assets/b08ae8fb-0fb1-418b-8edc-e286b59cb39a)
- 
- Log file outputs showing system and process monitoring details.
- 
- ![image](https://github.com/user-attachments/assets/e4991b42-90ff-4aa6-97bd-d4e403459183)
- 
- ![image](https://github.com/user-attachments/assets/2b728b7b-f914-4f2f-8c2f-98c2bd74aed8)
---

## Task 2: User Management and Access Control

### Objective:
Set up user accounts and configure secure access controls for the new developers.

### Steps:

1. **Created user accounts for Sarah and Mike:**
   ```bash
   sudo adduser sarah
   sudo adduser mike
2. **Created dedicated directories for both users:**
   
   ```bash
   sudo mkdir -p /home/sarah/workspace
   sudo mkdir -p /home/mike/workspace
   
4. **Set permissions: Ensure only Sarah and Mike can access their respective directories:**
   
   ```bash
   sudo chmod 700 /home/sarah/workspace
   sudo chown sarah:sarah /home/sarah/workspace
   sudo chmod 700 /home/mike/workspace
   sudo chown mike:mike /home/mike/workspace
   ```
   
5. **Implement password policies:Configure password expiration every 30 days**
   
   sudo chage -M 30 sarah
   sudo chage -M 30 mike
   
**Outputs**

![image](https://github.com/user-attachments/assets/af2e6257-7cb6-4927-96a9-cbaffd84ad97)

![image](https://github.com/user-attachments/assets/cdcca5ff-6533-486a-8767-d572c925f7d4)


**Task 3: Backup Configuration for Web Servers**

**Objective**

To automate backups for Apache and Nginx web servers, including configuration files and document roots, and verify the backup integrity.

**Steps**

**1.	Switch to user sarah**

      Sudo -u sarah -i
      
**2.	Apache (Sarah's server) Backup Configuration:**

      tar -czf ~/workspace/backup/apache_backup_$(date +%F).tar.gz /etc/apache2/ /var/www/html/

**3.	Switch to user Mike :**

     Sudo -u mike -i

**4.	Nginx (Mike's server) Backup Configuration:**

     tar -czf ~/workspace/backup/nginx_backup_$(date +%F).tar.gz /etc/nginx/ /usr/share/nginx/html/

**5.	Scheduled cron jobs:**
      
      Sarah's backup cron job:
         crontab -e
         0	0 * * 2 /path/to/apache_backup.sh
      Mike's backup cron job:
         crontab -e
         0 0 * * 2 /path/to/nginx_backup.sh
**6.	Verified backup integrity:**

      List contents of the compressed files:
          tar -tvf /backups/apache_backup_$(date +%F).tar.gz
          tar -tvf /backups/nginx_backup_$(date +%F).tar.gz
**Outputs:**

•	Backup files in /backups/ directory. 

![image](https://github.com/user-attachments/assets/33858abc-f95a-432d-bb5d-4c6270ef271c)

![image](https://github.com/user-attachments/assets/23b4c66a-d785-4c1b-8a8b-2a5567a04b04)

![image](https://github.com/user-attachments/assets/4c1849d6-1df3-4c32-8e81-e348dd606ff7)

![image](https://github.com/user-attachments/assets/8fbc094e-2133-42cd-aa44-8eb8233f8458)

•	Verification logs showing successful backup contents.

![image](https://github.com/user-attachments/assets/44a5a277-d21a-4a82-a064-fa3ed6e1c989)

![image](https://github.com/user-attachments/assets/0e2c0a6d-757f-4370-906a-134b714d6f86)

**Summary**

•	Successfully installed and configured monitoring tools (htop, nmon).

•	User accounts and secure directories set up for Sarah and Mike with enforced password policies.

•	Automated backups configured for Apache and Nginx servers with verified integrity.









     





    
   
