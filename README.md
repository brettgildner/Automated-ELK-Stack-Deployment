## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/file/d/1cVY9Z5iZbgCxEjB017IaD4wNvYBhG0ur/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Red-Team-NSG file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/brettgildner/Homework_13/blob/main/filebeat-playbook.yml                                                           

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing brings a greater degree of functionality to the application while restricting traffic to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
Filebeat: Monitors the logs and the locations that you've chosen to be sent to Elasticsearch/Logstash to be catalogued. 
Metricbeat: Documents the data and forwards it onto analyzing software you've selected.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.1.0.8   | Linux            |
| ELK-vm   | Server   | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.1.0.5   | Linux            |
| Web-2    | Server   | 10.1.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
68.224.187.248

Machines within the network can only be accessed by Jump-Box Provisioner.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump-Box | Yes                 | 20.83.100.208        |
| ELK-vm   | No                  | 10.1.0.8             |
| Web-1    | No                  | 10.1.0.8             |
| Web-2    | No                  | 10.1.0.8             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Infrastructure as Code (IAC) allows stable and scalable environments, consistency of configuration, easier documentation, increased speed and accountability, and reduced risk.

The playbook implements the following tasks:
- Configures the target VM to use more memory
- Installs docker.io, python3-pip, and docker
- Downloads the docker container sebp/elk:761
- Configures the container starting port mappings
- Starts the container and enables docker service on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="630" alt="VNET_diagram" src="https://user-images.githubusercontent.com/85353387/140572948-759e659b-833c-437a-95d7-e010487c19e7.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.1.0.5)
- Web-2 (10.1.0.6)

We have installed Filebeat and Metricbeat on the machines.
   
<img width="870" alt="Filebeat screenshot" src="https://user-images.githubusercontent.com/85353387/140571708-ad42acdc-a8a2-41eb-b34f-b3af384936f4.png">
<img width="905" alt="Metricbeat screenshot" src="https://user-images.githubusercontent.com/85353387/140571728-dbc7d4a1-fbd5-4d0b-ae89-aed5d8f2ff9c.png">

While monitoring, Filebeat uses harvesters (to individually read the content of a single file) and inputs (to manage the harvesters) to keep a state of each file it finds to be analyzed. Similarly, Metricbeat collects data and allows you to access it in a user-friendly format (such as CPU and memory usage, disk space and inbound/outbound traffic, as seen in the screenshot provided). 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy filebeat-configuration.yml to /etc/ansible/roles.
- Update filebeat-configuration.yml to include the ELK IP in lines 1106/1806, as formatted.
- Run the playbook, and navigate to http://13.82.175.97:5601/ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? filebeat-playbook.yml
-  Where do you copy it? /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
- _Which URL do you navigate to in order to check that the ELK server is running? http://13.82.175.97:5601/

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
