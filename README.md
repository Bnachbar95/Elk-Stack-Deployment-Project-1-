# Elk-Stack-Deployment-Project-1-
Full, tested, and working Elk Stack deployment using Microsoft Azure. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- The load balancer helps to ensure the availibilty and accessibilty of the environment by distributing incoming data to the web servers efficiently. Jump boxes allow for the adminitration of several systems to be easier and provide an additional layer between your internal assets and the outside enviroment. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system perfomance.
- Filebeat watches for log directories or specific log files. 
- Metricbeat monitors servers by collecting metrics from the system and other services that are running within the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4  | Linux(Ubuntu)    |
| Web-1    | Server    | 10.0.0.8  | Linux(Ubuntu)    |
| Web-2    | Server    | 10.0.0.7  | Linux(Ubuntu)    |
| Web-3    | Server    | 10.0.0.5  | Linux(Ubuntu)    |
| Elk VM   | Log Server| 10.1.0.4  | Linux(Ubuntu)    |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My personal IP address of my local machine.  

Machines within the network can only be accessed by the Jump Box Provisioner.
- The Ek Server can have access from my personal IP address of my local machine through port 5601. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |        Yes          |      Personal IP     |
| LBalancer|        Yes          |      Open            |
| Web-1    |         No          |      10.0.0.8        |
| Web-2    |         No          |      10.0.0.7        |
| Web-3    |         No          |      10.0.0.5        |
| Elk VM   |        Yes          |      Personal IP     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it can limit the amount of services running, any process can be more easily replicated, and installations and updates can be more efficient. 

The playbook implements the following tasks:
- Installs docker.io, pip3, and the docker module. 
- Increases the virtual memory. 
- Uses sysctl module 
- Downloads and launches the docker container 

The screenshot displayed above is the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 Server (10.0.0.5)
- Web-2 Server (10.0.0.6)

We have installed the following Beats on these machines:
- FileBeat
- Metric Beat

These Beats allow us to collect the following information from each machine:
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. 
- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. An example would be amount of CPU usage. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to the Web VM's.
- Update the /etc/ansible/hosts file to include the IP address of the Elk Server and webservers.
- Run the playbook, and navigate to http://[public_IP_ELK]:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- The Filebeat Configuration is the playbook and I copied it from /etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat.yml
- I updated the filebeat-config.yml to make Ansible run on a specific machine. I specified which machine by updating the host files with the correct IP addresses of the webservers and elkservers and then selecting which group to run on in Ansible. 
- I navigated to http://[public_IP_ELK]:5601/app/kibana to verify that the ELK server is running. 

To download the playbook, update the files, etc., run the following commands. 
- ssh into th Jump Box Provisioner using ssh username@ipaddress 
- docker run ansible container name 
- docker attach ansible container name 
- cd /etc/ansible 
- nano hosts file to update IP addresses on webservers or elkservers 
- nano ansible.cfg to change the name of the remote user
