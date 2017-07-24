##   Task. Zabbix. Basics

# 1.You should install and configure Zabbix server

<img src="pictures/Screenshot from 2017-07-24 12-40-12.png">
    Config page
# 2. Using Zabbix UI:
Create User group “Project Owners” 
Create User (example “Siarhei Beliakou”), assign user to “Project Owners”, set email
Add 2nd VM to zabbix: create Host group (“Project Hosts”), create Host in this group, enable ZABBIX Agent monitoring
Assign to this host template of Linux 
Create custom checks (CPU Load, Memory load, Free space on file systems, Network load)
Create trigger with Severity HIGH, check if it works (Problem/Recovery)
Create Action to inform “Project Owners” if HIGH triggers happen
