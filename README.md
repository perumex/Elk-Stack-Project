
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![VNET](https://github.com/perumex/Elk-Stack-Project/blob/master/Images/VNet%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Dvwa-playbook.yml
Elk-playbook.yml
Filebeat-playbook.yml
metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology. 

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly robust, in addition to restricting access to the network.
- What aspect of security do load balancers protect? What is the advantage of a jump box?

	As part of support for an HTTP web server, Load Balancers operate on layer 7 and distribute traffic to a collection of redundant servers so that any individual server will not be overwhelmed and crash (ie in the event of a DDos attack). A jump box allows an Admin access to the back end pool.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Data and system services.
- What does Filebeat watch for? 
analyzes/sorts logs
- What does Metricbeat record? 
provides system/service info

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| DVWA 1     |   Server     |   10.0.0.12     |  Linux     |
| DVWA 2     |     Server     |  10.0.0.11      |   Linux       |
| ELK     |    Monitor      |    10.0.0.4        |    Linux       |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.88.103.229

Machines within the network can only be accessed by SSH.
-Which machine did you allow to access your ELK VM? What was its IP address?
Jump Box from ip 76.88.103.229

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes            | 10.0.0.11, 10.0.0.12, 76.88.103.229    |
| DVWA 1     |  No          |   10.0.0.4, 10.0.0.5    |
| DVWA 2     |  No          |   10.0.0.4, 10.0.0.5    |
|  ELK       |      No           |  10.0.0.5                    |

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Having an automated script helps keep consistent configurations across installs/boxes.

The playbook implements the following tasks:
 - Install Docker
- Install pip
- Install Docker Python
- Increase virtual memory
- Download/Launch Docker Elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Install](https://github.com/perumex/Elk-Stack-Project/blob/master/Images/ELK%20docker.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.12 DVWA 1
- 10.0.0.11 DVWA 2

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine: 

-Filebeat collects all log information and makes it searchable.
-Metricbeat collects system info such as cpu and memory usage. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to DVWM.
- Update the Host file to include ELK server (10.0.0.4)
- Run the playbook, and navigate to Kibaba web page to check that the installation worked as expected.

- Which file is the playbook? Elk-Playbook.yml, filebeat-playbook.yml, metricbeat-playbook.yml
- Where do you copy it? They run off jump-box ansible
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
In /etc/ansible/     You update the host file with the IPs of the DVWMs under [webservers] and the ELK IP under [elkservers] this is how each playbook knows were to install. Filebeat/metricbeat playbooks install to webservers and elk-playbook installs to elkservers

- _Which URL do you navigate to in order to check that the ELK server is running?
  http://40.112.134.170:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

