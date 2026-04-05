# HeroVired_Linux_Assignment
Problem Statement 
Rahul, a Senior DevOps engineer at Tech Corp, needs to set up and manage development environments for two new developers, Sarah and Mike. The setup must ensure proper system monitoring, user management, troubleshooting capabilities, and automated backup procedures.
As a Fresher DevOps Engineer, you are assisting Rahul in implementing a secure, monitored, and well-maintained development environment that meets the organization’s operational and security standards. Additionally, Sarah and Mike are tasked with setting up automated backups for their respective web servers.

Task 1: System Monitoring Setup
Install and configure htop or nmon to monitor CPU, memory, and processes, using df and du for disk usage tracking, and identifying resource-intensive processes. Proper logging of system metrics and clear documentation of the setup are essential. 
Task 2: User Management and Access Control
Evaluation includes creating user accounts for Sarah and Mike with secure passwords, setting up isolated directories with appropriate permissions, and enforcing a password policy with expiration and complexity. Detailed documentation of user management steps is required. 
Task 3: Backup Configuration for Web Servers
Configure automated backups for Apache (/etc/httpd/, /var/www/html/) and Nginx (/etc/nginx/, /usr/share/nginx/html/), scheduling cron jobs to run every Tuesday at 12:00 AM, using the correct naming convention for backup files, and verifying backup integrity. Proper documentation and logs are necessary. 
Overall Report and Presentation
The report should clearly summarize implementation steps and challenges, including relevant screenshots or terminal outputs demonstrating task completion.


________________________________________
Tasks Detail:
Task 1: System Monitoring Setup
Objective: Configure a monitoring system to ensure the development environment’s health, performance, and capacity planning.
Scenario:
•	The development server is reporting intermittent performance issues.
•	New developers need visibility into system resource usage for their tasks.
•	System metrics must be consistently tracked for effective capacity planning.
Requirements:
1.	Install and configure monitoring tools (htop or nmon) to monitor CPU, memory, and process usage.
Command - sudo apt install htop -y
 
sudo apt install nmon -y
 
 
2.	Set up disk usage monitoring to track storage availability using df and du.
df -h
 
 

3.	Implement process monitoring to identify resource-intensive applications.
Create a simple monitoring script that logs CPU, memory, and top processes every 60 seconds.
#Create a Script file
sudo nano /usr/local/bin/monitor-resources.sh
#!/bin/bash
LOG_FILE="/var/log/system_monitor.log"
INTERVAL=60          # seconds between samples

mkdir -p "$(dirname "$LOG_FILE")"

while true; do
    echo "=== $(date) ===" >> "$LOG_FILE"

    # CPU and memory snapshot (top 5 lines)
    top -b -n1 | head -5 >> "$LOG_FILE"

    # Top 5 CPU intensive processes
    echo "Top CPU:" >> "$LOG_FILE"
    ps aux --sort=-%cpu | head -6 >> "$LOG_FILE"

    # Top 5 memory intensive processes
    echo "Top Memory:" >> "$LOG_FILE"
    ps aux --sort=-%mem | head -6 >> "$LOG_FILE"

    # Disk usage snapshot
    echo "Disk usage:" >> "$LOG_FILE"
    df -h | head -5 >> "$LOG_FILE"

    echo "" >> "$LOG_FILE"
    sleep "$INTERVAL"
done
 
#Make the script executable
sudo chmod +x /usr/local/bin/monitor-resources.sh
#Start in the background
nohup /usr/local/bin/monitor-resources.sh &
 




________________________________________
Task 2: User Management and Access Control
Objective: Set up user accounts and configure secure access controls for the new developers.
Scenario:
•	Two new developers, Sarah and Mike, require system access.
•	Each developer needs an isolated working directory to maintain security and confidentiality.
•	Security policies must ensure proper password management and access restrictions.
Requirements:
1.	Create user accounts for Sarah and Mike with secure passwords.
 

 
2.	Set up dedicated directories: 
o	Sarah: /home/Sarah/workspace
o	Mike: /home/mike/workspace
 
3.	Ensure only the respective users can access their directories using appropriate permissions.
 
 
 
Verifying user access
 
 

4.	Implement a password policy to enforce expiration and complexity (e.g., passwords expire every 30 days).
 
________________________________________
Task 3: Backup Configuration for Web Servers
Objective: Configure automated backups for Sarah’s Apache server and Mike’s Nginx server to ensure data integrity and recovery.
Scenario:
•	Sarah is responsible for managing an Apache web server.
•	Mike is responsible for managing a Nginx web server. 
•	Both servers require regular backups to a secure location for disaster recovery.
Requirements:
1.	Sarah and Mike need to automate backups for their respective web server configurations and document roots: 
o	Sarah: Backup the Apache configuration (/etc/httpd/) and document root (/var/www/html/).
o	Mike: Backup the Nginx configuration (/etc/nginx/) and document root (/usr/share/nginx/html/).

Create backup Directories
sudo chown sarah:sarah /home/Sarah/backups
sudo chown mike:mike /home/Mike/backups
 
Create Backup Script for Sarah (Apache)
nano /home/Sarah/apache_backup.sh
 
Create Backup Script for Mike (Nginx)
nano /home/Mike/nginx_backup.sh
 

2.	Schedule the backups to run every Tuesday at 12:00 AM using cron jobs.



0 0 * * 2 /home/Mike/nginx_backup.sh

0 0 * * 2 /home/mike/apache_backup.sh    
   
3.	Save the backups as compressed files in /backups/ with filenames including the server name and date (e.g., apache_backup_YYYY-MM-DD.tar.gz).
 
4.	Verify the backup integrity after each run by listing the contents of the compressed file.
 


