# Azure-Virtual-Network-ELK-Deployment

The files in this repository were used to configure the network depicted below
[Project 1 Red-Team Network Diagram](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Diagram/Azure_Cloud_Virtual_Network_with_ELK_Deployment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

- [Ansible Playbook](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/my-playbook1.yml)
- [Ansible Hosts](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/hosts.yml)
- [Ansible Configuration](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/ansible.cfg)
- [Ansible ELK Installation and VM Configuration](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/ansible.cfg)
- [Ansible Filebeat Playbook](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/ELK_Stack/filebeat-playbook.yml)
- [Ansible Filebeat Config file](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/filebeat-config.yml)
- [Ansible Metricbeat Playbook](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/ELK_Stack/metricbeat-playbook.yml)
- [Ansible Metricbeat Config file](https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Ansible/metricbeat-config.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _available_, in addition to restricting _traffic_ to the network. 

- What aspect of security do load balancers protect? 
  
  Answer: _Availability, Web Traffic, Web Security_

- What is the advantage of a jump box? 
  
  Answer: _Automation, Security, Network Segmentation, Access Control_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _data_ and system _logs_.

- What does Filebeat watch for? _Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing._

- What does Metricbeat record? _Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function     | IP Address               | Operating System |
|----------------------|--------------|--------------------------|------------------|
| Jump-Box-Provisioner | Gateway      | 10.0.0.4 /20.70.170.56   | Linux            |
| Web1                 |Web Server    | 10.0.0.5                 | Linux            |
| Web2                 |Web Server    | 10.0.0.6                 | Linux            |
| ELK                  |ELK Server    | 10.1.0.4 /20.213.244.104 | Linux            |
| Load Balancer        |Load Balancer | Static External IP       | Linux            |
| Workstation          |Access Control| External IP or PublicIP  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Elk Server_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
- _Workstation Public IP through TCP 5601._

Machines within the network can only be accessed by _Workstation_ and _Jump-Box-Provisioner_.
Which machine did you allow to access your ELK VM? What was its IP address?
- _Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22_ 
- _Workstation Public IP via port TCP 5601_

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible  | Allowed IP Addresses                  |
|-------------|----------------------|---------------------------------------|
| Jump Box    |      No              | Workstation Public IP on SSH  22      |
|   Web1      |      No              | 10.0.0.4 on SSH  22                   |
|   Web2      |      No              | 10.0.0.4 on SSH  22                   |
|ELK Server   |      No              | Workstation Public IP using TCP  5601 |
|Load balancer|      No              | Workstation Public IP on  HTTP 80     |   

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because _Ansible lets you quickly and easily deploy multitier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in._

*The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

	- First SSH into the Jump-Box-Provisioner (ssh redadmin@publicIP)
	- Start/Attached to the ansible docker (sudo docker start  tender_morse)/(sudo docker attach tender_morse)
	- Went to /etc/ansible/roles directory and created the ELK playbook (Elk_Playbook.yml)
	- Ran the Elk_Playbook.yml in that same directory (ansible-playbook Elk_Playbook.yml)
	- SSH into the ELK-VM to verify the server is up and running.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
[]https://github.com/bilee83/Azure-Virtual-Network-ELK-Deployment/blob/main/Linux/ELK-VM%20Docker%20PS.png


### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
 - Web1 : 10.0.0.5
 - Web2 : 10.0.0.6

We have installed the following Beats on these machines: 
 - ELK Server, Web1 and Web2
 - The ELK Stack Installed are: _FileBeat and MetricBeat_

These Beats allow us to collect the following information from each machine:
 - Filebeat:    _log events_
 - Metricbeat:  _metrics and system statistics_

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

---Filebeat---

- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
- Run the playbook, and navigate to http://20.213.244.104:5601/ (ELK-VM public IP) to check that the installation worked as expected.

---Metricbeat---

- Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 and 96.
- Run the playbook, and navigate to http://20.213.244.104:5601/ (ELK-VM public IP) to check that the installation worked as expected.

_Answer the following questions to fill in the blanks:_

- _Which file is the playbook? filebeat-playbook.yml
- _Where do you copy it? /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts file (IP of the Virtual Machines). 
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on? I have to specify two separate groups in the etc/ansible/hosts file. One of the groups will be webservers which has the IPs of the VMs that I will install Filebeat to. The other group is named elkservers which will have the IP of the VM I will install ELK to.
- _Which URL do you navigate to in order to check that the ELK server is running? http://20.213.244.104:5601/ 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

      -------Filebeat---------

	- To create the filebeat-configuration.yml file: nano filebeat-configuration.yml. For this, I used the filebeat configuration file template.
	
	- To create the playbook: nano filebeat-playbook.yml
	
      ---
 	 - name: installing and launching filebeat
    	   hosts: webservers
           become: true
           tasks:

    	   - name: download filebeat deb
      	     command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.7.1-amd64.deb

    	   - name: install filebeat deb
      	     command: dpkg -i filebeat-7.7.1-amd64.deb

    	   - name: drop in filebeat.yml
      	     copy:
       	       src: ./files/filebeat-configuration.yml
       	       dest: /etc/filebeat/filebeat.yml

    	   - name: enable and configure system module
      	     command: filebeat modules enable system

    	   - name: setup filebeat
      	     command: filebeat setup

    	   - name: start filebeat service
      	    command: service filebeat start
	---
	-To run the playbook: ansible-playbook filebeat-playbook.yml
	
	* In order to run the playbook, you have to be in the directory the playbook is at, or give the path to it (ansible-playbook /etc/ansible/roles/filebeat-playbook.yml
	
	
	-------Metricbeat-------
	
	- To create the metricbeat-configuration.yml file: nano metricbeat-configuration.yml. For this, I used the metricbeat configuration file template.
	
	- To create the playbool: nano metricbeat-playbook.yml
	
	---
	  - name: installing and lunching metricbeat
	    hosts: webservers
	    become: true
	    tasks:
	    
	  - name: download metricbeat deb
	    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.7.1-amd64.deb
	    
	  - name: install metricbeat deb
	    command: sudo dpkg -i metricbeat-7.7.1-amd64.deb
	    
	  - name: drop in metricbeat.yml
	    copy:
	      src: /etc/ansible/roles/files/metricbeat-configuration.yml
	      dest: /etc/metricbeat/metricbeat.yml
	      
	   - name: enable and configure system module
	     command: metricbeat modules enable system
	     
	   - name: setup metricbeat
	     command: metricbeat setup
	     
	   - name: start metricbeat service
	     command: service metricbeat start
	     
	   ---
	   
	   - To run the playbook: ansible-playbook metricbeat-playbook.yml
	   
	   * To order to run the playbook, you have to be in the directory the playbook is at, or give the path to it (ansible-playbook /etc/ansible/roles/metricbeat-playbook.yml
