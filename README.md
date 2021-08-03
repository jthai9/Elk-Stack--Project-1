Jonathan Thai
# Elk-Stack--Project-1
Elk Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

		- https://github.com/jthai9/Elk-Stack--Project-1/blob/main/Diagrams/Diagram%202.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

		- Ansible/install.elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
		- Load balancer prevent overloading a server. Its main job is to distributes network or application traffic accross many servers. 
		- A jump box is a secure computer that is used to launch any administrative task or use as a point to connect to other servers or untrusted environments.
		
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- _TODO: What does Filebeat watch for?_
		- Filebeat monitors log files  
- _TODO: What does Metricbeat record?_
		- It records metrics and statistics data 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Server   | 10.0.0.7   | Linux            |
| Web 2    | Server   | 10.0.0.6   | Linux            |
| Elk VM   | Sever    | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
		- 20.85.216.26
		
Machines within the network can only be accessed by Jump-Box-Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
		- Jump-Box-Provisioner
		- 10.1.0.5 (Private IP address for the Elk VM)
A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | Yes/No              | 10.0.0.1 10.0.0.2    |
| Web 1       | No                  | 10.0.0.7             |
| Web 2       | No                  | 10.0.0.6             |
|Elk JumpBox-2| No                  | 10.1.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
		- Using the YAML playbooks which is use to automate the configuration of multiple servers.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
		- Ssh into the Jump-Box-Provisioner.
		- Start and attach the docker which has ansible.
		- Navigate into /etc/ansible and create the ELK installation playbook.
		- Add the the private IP address into the hosts file.
		- Execute the comman ansible-playbook "install.elk.yml" and ssh into the elk to see if it works. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

		- Screenshots/Elk Screenshot.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
		- Web 1 (40.87.26.156/10.0.0.7)
		- Web 2 (40.87.26.156/10.0.0.6)

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
		- Filebeat 
		- Metricbeat 

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
		- Filebeat collect log files 
				- An example of filebeat logs from apache
		- Metricbeat collect the metrics and statistics of the servers	
				- An example of metricbeat is CPU usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/roles/files.
- Update the filebeat-config.yml file to include Elk server private IP in the appate lines 
- Run the playbook, and navigate to http://20.97.216.245:5601/app/kibana#/home to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- Which file is the playbook? filebeat-playbook.yml
- Where do you copy it? /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? hosts file
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? By adding two different groups inside the hosts file. One is webservers group and the second is the elk group.
- Which URL do you navigate to in order to check that the ELK server is running? http://20.97.216.245:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
