## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/73618945/118374166-e0ab7200-b577-11eb-9d56-d4cb4bbfe404.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the beat files may be used to install only certain pieces of it, such as Filebeat.

  https://github.com/Aakris/13ElkStackProject/blob/main/Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting DDOS attacks to the network.
- Load balancers are important because they increase the amount of space for concurrent users and makes the application more reliable. If one were to fail or be attacked it would shift the traffic onto another server instead of going down completely.
- Jump box is important for this setup because it acts as a place for admins to connect to first before doing anything administrative or anything important. It also acts as a barrier if there was a situation where we needed to connect to other servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat is used to monitor and collect whatever data you want and send it to either Elasticsearch or Logstash, whichever you prefer. 
- Metricbeat takes metrics and statistics from the operating system of the services on the server. Then just like FIlebeat you can send it to Elasticsearch or Logstash

The configuration details of each machine may be found below.
_______________________________________________________
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| WEB1     | Server   | 10.0.0.5   | Linux            |
| WEB2     | Server   | 10.0.0.6   | Linux            |
| WEB3     | Server   | 10.0.0.7   | Linux            |
| ELK      | Logs     | 10.1.0.4   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Put the main ip you would use to access this
Machines within the network can only be accessed by the Jumpbox Container.
- I allowed my Jumpbox to access this and manage the playbooks
Jumpbox 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1             |
| Web1,2,3 | Yes                 | 10.0.0.5/6/7         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually.
- Automating this process is worthwile in case you ever want to set it up again. You do not have to spend the time and resources to create it again when the playbook is right there ready to be used. There is only room for human error in the initial setup of the playbook which is another plus

The playbook implements the following tasks:
- Installs docker.io
- Installs pip3
- Increases memory
- Downloads and launches Docker Container
- Enables Docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/73618945/118352680-e2e1e200-b51f-11eb-89f6-50c2bf4fe583.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1
- Web2
- Web3

We have installed the following Beats on these machines:
- Metricbeat and Filebeat

These Beats allow us to collect the following information from each machine:
- Linux logs
- Host Metadata
- Cloud Metadata

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Elk-Server-Deployment.yml file to /etc/ansible/ directory
- Update the hosts file to include the ip addresses of the elk machine(s)
- Run the playbook, and navigate to webservers to check that the installation worked as expected.
- It should look similarly to this
- [webservers]
- 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
- 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
- 10.0.0.7 ansible_python_interpreter=/usr/bin/python3

### Finishing up

Make sure to update the hosts file to include the elk machine, you can fit it below the webservers (seen above)
- [elk]
- 10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Both of the playbooks can be located below 
- filebeat-configuration.yml https://github.com/Aakris/13ElkStackProject/blob/main/Ansible/filebeat-configuration.yml
- filebeat-playbook.yml https://github.com/Aakris/13ElkStackProject/blob/main/Ansible/filebeat-playbook.yml
- metricbeat-configuration.yml https://github.com/Aakris/13ElkStackProject/blob/main/Ansible/metricbeat-configuration.yml
- metricbeat-playbook.yml https://github.com/Aakris/13ElkStackProject/blob/main/Ansible/metricbeat-playbook.yml
-run - "ansible-playbook filebeat-playbook.yml" in the folder where ansible is
-run - "ansible-playbook metricbeat-playbook.yml" 
After that it should install them and leave .deb files in their place where they have been installed!

- Finally go to http://10.1.0.4:5601 to check if your kibana is running correctly
