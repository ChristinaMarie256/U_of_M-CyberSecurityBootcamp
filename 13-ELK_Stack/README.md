## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/IMAGES/Net_Diagram.jpg)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook YAML files may be used to install only certain pieces of it, such as Filebeat.

 - [elk-install_playbook.yml](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/elk-install_playbook.yml)
 - [filebeat-playbook.yml](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/filebeat-playbook.yml)
 - [metricbeat-playbook.yml](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build



### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performace.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | DVWA VM  | 10.0.0.5   | Linux            |
| Web-2    | DVWA VM  | 10.0.0.6   | Linux            |
| Web-3    | DVWA VM  | 10.0.0.7   | Linux            |
| ELK VM   | ELK Stack| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:

47.232.50.214

Machines within the network can only be accessed by SSH on Port 22 from the following IP address:

10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 47.232.50.214        |
| DVWA VMs | No                  | 10.0.0.4             |
| Elk VM   | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the same configuration can be used on multiple machines.

The ELK playbook implements the following tasks:

- Install Docker.io
- Install Python3-pip
- Install docker module
- Increase & use more virtual memory
- Download and launch the Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- 10.0.0.5 (DVWA Web-1)
- 10.0.0.7 (DVWA Web-2)
- 10.0.0.8 (DVWA Web-3)

We have installed the following Beats on these machines:
- filebeat-7.4.0-amd64.deb
- metricbeat-7.4.0-amd64.deb



These Beats allow us to collect the following information from each machine:
- **Filebeat:** used to detect file system changes using Apache logs.
- **Metricbeat:** used to detect system metrics changes, SSH login attempts, and CPU/RAM statistics. 

### Using the Playbooks

- [Filbeat Configuration YAML](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/filebeat-configuration.yml)
- [Filebeat playbook](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/filebeat-playbook.yml)
- [Metricbeat Configuration YAML](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/metricbeat-configuration.yml)
- [Metricbeat playbook](https://github.com/ChristinaMarie256/U_of_M-CyberSecurityBootcamp/blob/main/13-ELK_Stack/Ansible/metricbeat-playbook.yml) 


In order to use the playbooks, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks to the Ansible Control Node.
- Update the /etc/ansible/hosts file to include the Web Virtual Machines: 10.0.0.5; 10.0.0.6; 10.0.0.7
- Update the /etc/ansible/hosts file to include the ELK Virtual Machine: 10.1.0.4
- Run the playbooks with the commands below, then navigate to Kibana at 10.0.0.8:5601 to check that the installation worked as expected.

`cd/ etc/ansible`

`ansible-playbook elk-install_playbook.yml elk`

`ansible-playbook filebeat-playbook.yml webservers`

`ansible-playbook metericbeat-playbook.yml webservers` 

`curl http://10.0.0.8:5601`