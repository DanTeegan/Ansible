# Creating Ansible Playbook
## Adhog commands
- ansible all -m shell -a "ifconfig" finding ip address
- ansible all -m shell -a "env" # find environment variables
- ansible all -a "uptime" # checking uptime for all machines
- ansible all -a "df -h" # Checking disk space for all machines 
- ansible all -a "mpstat -P all" # Checking all processes for all machines

## What are they?
- Automates to tasks in multiple servers
- Playbooks are written in YMAL .ymal or .yml extention. YAML Syntax – YAML file starts with --- three dashes (---)

## Why should we use them/benefits?
For configuration management – install programs – update programs – etc..

## How to create a playbook?

## What can we do with playbooks?
- Configuration management

## If we have adhog commands why do we need to use playbooks?
- Because in 1 playbook we can install nginx on 50 servers


##### 1) In your controller go into the root using ```sudo su``` and then create the filename with the .yml or ymal file extention

![](images/a16.png)

##### 2) Syntax to install nginx is seen below. It will install nginx on the web as seen in the hosts.

![](images/a17.png)

##### 3) Then save the file and leave the root using the exit command. Once out of the root use the command 
``` ansible-playbook install_nginx_on_web.yml ```

![](images/a18.png)