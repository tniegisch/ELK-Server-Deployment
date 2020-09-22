## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(ELK-Server-Deployment/Images/AZ_NET_ELK.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - Install_DVWA.yml
  - ELK_Playbook.yml
  - Beats_Playbook.yml

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the containers and system logs.

The configuration details of each machine may be found below.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4   | Linux            |
| Web-01    | DVMA     | 10.0.0.8   | Linux            |
| Web-02    | DVMA     | 10.0.0.9   | Linux            |
| Web-03    | DVMA     | 10.0.0.11  | Linux            |
| XCORP-ELK | ELK      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address: 104.143.50.247

Machines within the network can only be accessed by the Jump Box machine via SSH @ IP 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses & Ports     |
|-----------|---------------------|----------------------------------|
| Jump Box  | Yes                 | 104.143.50.247:22                |
| Web-01    | No                  | 10.0.0.4:22, 10.1.0.4:5601       |
| Web-02    | No                  | 10.0.0.4:22, 10.1.0.4:5601       |
| Web-03    | No                  | 10.0.0.4:22, 10.1.0.4:5601       |
| XCORP-ELK | Yes                 | 10.0.0.4:22; 104.143.50.247:5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it eliminated the likelyhood of errors and allowed the services to be installed quickly.

The playbook implements the following tasks:
- Install docker.io
- Install pip
- Increase Virtual Memory
- Assign more memory
- Download and Launch ELK Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
(ELK-Server-Deployment/Images/ELK_Docker_PS.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.9
- 10.0.0.11

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects system logs that we can use to see machine uptime and connections
- Metricbeat collects metrics from the docker containers and can tell us when containers are started and stopped

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK_Playbook.yml file to /etc/ansible/roles.
- Update the hosts file to include '[elk]' group and '[Internal IP of ELK MV] ansible_python_interpreter=/usr/bin/python3'
- Run the playbook, and navigate to [ELK Public IP]:5601 to check that the installation worked as expected.

