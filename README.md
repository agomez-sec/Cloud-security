Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
 
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the IAC yml file may be used to install only certain pieces of it, such as Filebeat.
•	Elk-playbook.yml
•	Filebeat-playbook.yml
This document contains the following details:
•	Description of the Topology
•	Access Policies
•	ELK Configuration 
o	Beats in Use
o	Machines Being Monitored
•	How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly redundant in addition to restricting access to the network.
•	Load balancer protect us against a DDos attack or any situation where one of our webservers goes down, we have redundancy with our other 2 VMs.
•	Advantage of our jumpbox is that is allows us to connect via ssh to our ansible container that contains our provisioner Ansible. Within Ansible we’re able to ssh into any of our 3 VMs
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system any traffic going through.
•	The filebeat is used to watch all log files as well as collect events and makes its visible through Kibana
•	From the services running on the server , metricbeats collect metric and statistical data.
VM NAME	FUNCTION	IP ADDRESS	OS
JUMP-BOX	GATEWAY	10.0.0.7	LINUX
VM1	Running DVWA	10.0.0.8	LINUX
VM2	Running DVWA	10.0.0.9	LINUX
VM3	Running DVWA	10.0.0.10	LINUX
ELKVM	Running Elk	10.2.0.5	LINUX

Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the JUMPBOX machine can accept connections from the Internet. Access to this machine is only allowed from the our personal IP address:
Machines within the network can only be accessed by ssh with the proper ssh key
•	The ELKVM on (10.2.0.5) can only be accessed via jumpbox(10.0.0.7)
A summary of the access policies in place can be found in the table below.


NAME	PUBLICLY ACCESSIBLE	IP ADDRESS ALLOWED
JUMP-BOX	NO	PERSONAL IP 
VM1	NO	10.0.0.8
VM2	NO	10.0.0.9
VM3	NO	10.0.0.10
ELKVM	NO	10.2.0.5 AND PERSONAL IP

Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
•	Using an Anisable playbook we can update and mange multiple machine on our network making it quick in easy, this also prevents any human error that may occur when configuring vm’s individually. 
The playbook implements the following tasks:
•	First we will need to create a new VM. The public ip address will be used to access Kibana via the web through port 5601 and HTTP. The private ip address will allow us to ssh into the ELK server using our JUMPBOC VM (10.0.0.7)
•	Through the Ansible host.config file a new group will need to be added [ELKserever] or a known name, and the private IP will need to be added under this new group.
•	Creating an ansible playbook(elk.yml) will download, install and configure the new ELKVM via port 5601
•	Once running the playbook you should be able access the ELKVM using the personal ip and port 5601 which roles were configures in the ELK-nsg. Using the jump-box vm we can ssh into the ELK server to verify that the elk service is running.

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.





Target Machines & Beats
This ELK server is configured to monitor the following machines:
•	The machines monitored my the ELKVM server are the following:
o	VM1
o	VM2
o	VM3
We have installed the following Beats on these machines:
o	VM1
o	VM2
o	VM3
Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
•	Copy the filebeat-playbook.yml file to /etc/ansible/roles/files directory.
•	Update the configuration file to include the new group [ELKserver] as well as its private IP
•	Run the playbook, and navigate to the ELK server via ssh to check that the installation worked as expected and it is running
•	You can check two location and make sure the ELK server is running
o	Use the public ip address and make sure the site is up and running
o	Ssh into the ELVM through the jumpbox vm
