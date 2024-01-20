# LW-Anisble-EX180

# Introduction:

In this project, I will demonstrate the power of ansible to configure webservice and load-balancer to the dedicated instances and access webpage with the help of loadbalancer’s IP address.

# Requirements:

AWS account with aws_access_key 
Ansible Installed in controller node

# Setup

Step 1: On the controller node we will open inventory file located at /etc/anssible/hosts.

Step 2: In this file we will add the ip address of the target nodes, ec2 private key file path, ansible connection=ssh & username. we wil use groups as there are loadbalancers and webservers system so we use  two groups, add ip address of load balancer under lb group and ip of webservers under webdervers group. 

Step 3: Now create a project directory using mkdir ansible command & move inside ansible

Step 4: we will create role using the below command
$ ansible-galaxy role init lbrole (name of role)
$ ansible-galaxy role init webrole (name of role)

Step 5: The above command will create two directories which will have multiple other directories to write variables (in vars/main.yml file), handlers (in handlers/main.yml file), tasks (in tasks/main.yml file), template files (inside templates directory) etc.

Step 6: The default path of the role is /etc/ansible/roles. If the role is installed in any different path, that need to be mentioned in ansible configuration file after roles_path. Here, I have used my home directory as the roles_path and mentioned the same in config file.
roles_path=/home/arun/anuj/lwProjects/ansible:{{ ANSIBLE_HOME ~ "/roles:/usr/share/ansible/roles:/etc/ansible/roles" }}

Step 7: First we will setup the webserver role so we will open the webrole inside webrole we mill move to tasks folder and open main.yml file create our tasks to install and configure apache webserver.

Step 8: Now we will setup the load balancer role so we will open lbrole inside lbrole we mill move to tasks folder and open main.yml file create our tasks of installing, configuring & starting the services of HAProxy.

Step 9: we will create a handlers so open the main.yml file inside handler directory and write the code to restart haproxy service.

Step 10: In template folder we will copy the haproxy.cfg file as haproxy.cfg.j2 and write the logic of dynamic scaleup and scaledown. 

Step 11: Create a playbook setup.yml out of all these folders from where we can execute the ansible commands to run there roles.
$ ansible-playbook setup.yml

This command wil run the playbook 

Step 12: Now go to aws to copy the public ip address of load balancer instance and edit the security group to allow port 80 & 5000 to connect from anywhere. 

Step 13: Open web browser and paste the ip address of load balancer instance with 5000 as by default port number of HAProxy.
