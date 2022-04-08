# Azure-Virtual-Network-ELK-Deployment

The files in this repository were used to configure the network depicted below
![Azure_Cloud_Virtual_Network_with_ELK_Deployment](https://user-images.githubusercontent.com/93458722/162332741-27e08b0c-16df-4a72-8493-f4d5f34287e3.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

- [Ansible Playbook]
- [Ansible Hosts]
- [Ansible Configuration]
- [Ansible ELK Installation and VM Configuration]
- [Ansible Filebeat Playbook]
- [Ansible Filebeat Config file]
- [Ansible Metricbeat Playbook]
- [Ansible Metricbeat Config file]

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
| Jump-Box-Provisioner | Gateway      | 10.0.0.4 /52.242.18.55   | Linux            |
| Web1                 |Web Server    | 10.0.0.5                 | Linux            |
| Web2                 |Web Server    | 10.0.0.6                 | Linux            |
| ELK                  |ELK Server    | 10.1.0.4 /52.138.103.192 | Linux            |
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


