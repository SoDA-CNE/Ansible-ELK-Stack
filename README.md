## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/diagrams/azure_elk.png

These files have been tested and used to generate a live ELK deployment on Azure. 
Follow each step to setup the environment and configurations. 
Once installed added the individual parts to the ELK stack such as Filebeat.

/ansible/install-elk.yml

BEGIN HERE

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
Load balancers help protect the servers from system attacks that might compromise its availability. 
If one server is brought down from a DoS attack or has reached its processing capacity, the load balancer will send traffic to the remaining servers. 
The Advantage of a jump box is to limit access to the other servers from a single point within the network security environment._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the servers and system network.
- Filebeat collects data about the file system.
- Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.

| Name                 | Function              | IP Address | Operating System |
|----------------------|-----------------------|------------|------------------|
| Jump-Box-Provisioner | Jump Box Gateway      | 10.0.0.4   | Linux            |
| Web-3                | web application       | 10.0.0.7   | Linux            |
| Web-4                | web application       | 10.0.0.8   | Linux            |
| Web-5                | web application       | 10.0.0.9   | Linux            |
| Elk-VM               | Elk Application Stack | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the [jump-box-provisioner] machine can accept ssh connection from the Internet. Access to this machine is only allowed from the following IP addresses:
89.187.182.174

Machines within the network can only be accessed by other machines within the network for "neighborly jumping".
The Elk-VM can only be accessed by any machine on the 10.0.0.0/24 subnet using ssh, or by a single IP 89.187.182.174:5601 

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Address         |
|----------------------|---------------------|----------------------------|
| Jump-Box-Provisioner | Yes                 | 89.187.182.174             |
| Web-3                | Yes                 | 10.0.0.4,89.187.182.174    |
| Web-4                | Yes                 | 10.0.0.4,89.187.182.174    |
| Web-5                | Yes                 | 10.0.0.4,89.187.182.174    |
| Elk-VM               | Yes                 | 10.0.0.0/24,89.187.182.174 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
the configuration will remain consistent for each deployment.
- The main advantage for using ansible is rapid configuration and automated installation across the architectures.

The playbook implements the following tasks:
- ... Install Docker
- ... Install Python
- ... Download Elk Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
ansible/Images/docker_ps_output.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8
- 10.0.0.9_

We have installed the following Beats on these machines:
- 10.0.0.7 
- 10.0.0.8 
- 10.0.0.9_

These Beats allow us to collect the following information from each machine:
Filebeat collects and parses log files from various systems using their default log locations. 
E.g. The WinlogBeat collects Windows event logs and could present security events such as logon success and failures.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible.
- Update the "hosts" file to include the host groups of ip targets, and revise the ansible.cfg file witht the appropriate remote user
- Run the playbook, and navigate to public IP of the Elk server using port 5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
install-elk.yml
It is copied to the ElK-VM Container

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
[hosts]
You modify the hosts file and create a grouping / collection of hosts listed under [groupName]. Within the playbook the [groupName] is referenced for each specific intended play.

- _Which URL do you navigate to in order to check that the ELK server is running?
public IP:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
