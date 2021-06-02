## Project 1: ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/Rkelley6045/Elk-stack/blob/main/Diagrams/Proj.%201%20Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[Filebeat-playbook](https://github.com/Rkelley6045/Elk-stack/blob/main/Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. What aspect of security do load balancers protect? What is the advantage of a jump box?
  - The load balancing off-loading function helps protect the application from DDoS attacks by distributing traffic across our three virtual machines. The Jump Box acts a single entry point we can secure and monitor which in turn helps protect the virtual machines from public exposure. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performance.
- What does Filebeat watch for?
  - It is a logging agent designed to tail generated log files and forward the data to Logstash for advanced processing or Elasticsearch for indexing. 
- What does Metricbeat record?
  - Metricbeat periodically collects metrics from the operating system and from services running on the server. It takes those metrics and statistics and outputs them to Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|Name      | Function  | IP Address     | Operating System        |
|----------|-----------|----------------|-------------------------|
| Jump Box |  Gateway  | 10.0.0.4       | Linux Ubuntu 18.04.5    |
| DVWA-VM1 |  VM       | 10.0.0.7       | Linux Ubuntu 18.04.5    |
| DVWA-VM2 |  VM       | 10.0.0.8       | Linux Ubuntu 18.04.5    |
| DVWA-VM3 |  VM       | 10.0.0.9       | Linux Ubuntu 18.04.5    |
| ELK-VM   |  ELKStack | 10.1.0.4       | Linux Ubuntu 18.04.5    |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
162.245.132.25

Machines within the network can only be accessed by port 22.
- The Jump Box VM is the only machine that can access the ELK VM and that is via IP 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | No                  | 162.245.132.25       |
| DVWA-VMs  | No                  | 10.0.0.4             |
| ELK Stack | No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible's automation simplifies the configuration task which can be complex. This allows system administrators and developers to keep up with scaling while also freeing up their time to increase their efficency/value to their organization. 

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install Docker module
- Increase virtual memory for ELK VM
- Download and launch docker elk container
- Enable sevice docker on boot

[Elk install](https://github.com/Rkelley6045/Elk-stack/blob/main/Ansible/install-elk.yml)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps output](https://github.com/Rkelley6045/Elk-stack/blob/main/DockerConfirm/DockerPSOutput.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:
- filebeat-7.6.1 (amd64)
- metricbeat-7.6.1 (amd64)

These Beats allow us to collect the following information from each machine:
- Filebeat collects 
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Filebeats Config](https://github.com/Rkelley6045/Elk-stack/blob/main/BeatsConfigFiles/filebeat-config.yml) to the anisble directory on your VM.
- Update the hosts file to include webservers 10.0.0.7, 10.0.0.8, 10.0.0.9 and Elk 10.1.0.4.
![alt text](https://github.com/Rkelley6045/Elk-stack/blob/main/HostFile/Host%20File.png)
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- Which file is the playbook? Where do you copy it?_
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
