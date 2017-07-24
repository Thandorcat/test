#  Task. Zabbix. Basics

# 1.You should install and configure Zabbix server

<img src="pictures/Screenshot from 2017-07-24 12-40-12.png">

Config page
 
# 2. Task 1:

## Create User group “Project Owners” 

<img src="pictures/Screenshot from 2017-07-24 13-44-24.png">

## Create User (example “Siarhei Beliakou”), assign user to “Project Owners”, set email

<img src="pictures/Screenshot from 2017-07-24 13-45-37.png">

<img src="pictures/Screenshot from 2017-07-24 13-47-28.png">


## Add 2nd VM to zabbix: create Host group (“Project Hosts”), create Host in this group, enable ZABBIX Agent monitoring

<img src="pictures/Screenshot from 2017-07-24 14-33-09.png">

<img src="pictures/Screenshot from 2017-07-24 14-38-20.png">

## Assign to this host template of Linux 

<img src="pictures/Screenshot from 2017-07-24 14-39-38.png">

<img src="pictures/Screenshot from 2017-07-24 14-42-48.png">

## Create custom checks (CPU Load, Memory load, Free space on file systems, Network load)

<img src="pictures/Screenshot from 2017-07-24 17-29-29.png">

<img src="pictures/Screenshot from 2017-07-24 17-31-57.png">

<img src="pictures/Screenshot from 2017-07-24 17-36-53.png">

<img src="pictures/Screenshot from 2017-07-24 18-39-45.png">

## Create trigger with Severity HIGH, check if it works (Problem/Recovery)

## Create Action to inform “Project Owners” if HIGH triggers happen
