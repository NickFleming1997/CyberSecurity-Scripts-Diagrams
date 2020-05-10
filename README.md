## Automated ELK Stack Deployment
 
The files in this repository were used to configure the network depicted below.
 
![path for your diagram](blob/master/Images/network_diagram.png.png)
 
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the (install-elk.yml) file may be used to install only certain pieces of it, such as Filebeat.
 
  - Enter the playbook file. /etc/ansible/roles/filebeat-playbook.yml
 
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
 
 
### Description of the Topology
 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
 
Load balancing ensures that the application will be highly (fault resistant), in addition to restricting (traffic) to the network.
- : What aspect of security do load balancers protect? (Availability)  What is the advantage of a jump box? (control of multiple Virtual machines/containers in one location) 
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the (servers or applications) and system (system logs).
-What does Filebeat watch for? (Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.)
-What does Metricbeat record? (metricbeat uses the system module which collects server system metrics, such as CPU and memory usage, network, and so forth.)
 
The configuration details of each machine may be found below.
 
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway        | 138.91.187.196| Linux(Ubuntu 18.04)|
| DVWA 1   | training       | 40.112.185.41 | Linux(Ubuntu 18.04)|
| DVWA 2   | training       | 138.91.189.25 | Linux(Ubuntu 18.04)|
| Elkserver| log management | 52.240.59.170 | Linux(Ubuntu 18.04)|
 
### Access Policies
 
The machines on the internal network are not exposed to the public Internet. 
 
Only the (Jump-Box) machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Add whitelisted IP addresses (40.112.185.41, 138.91.189.25, 107.10.234.176)
 
 
Machines within the network can only be accessed by (Jump-box).
-Which machine did you allow to access your ELK VM? What was its IP address?
Local PC (107.10.234.176)
 
A summary of the access policies in place can be found in the table below.
 
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | no                  | any with ssh setup   |
| DVWA1&2  | yes                 | 107.10.234.176       | 
| Elkserver| yes                 | 107.10.234.176, 40.112.185.41,138.91.189.25|
 
### Elk Configuration
 
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible? (saves time and is consistent, the configuration can also be copied to other machines)
 
The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- (The first three tasks are installing docker.io, docker module and python-pip)
- (The fourth task is increasing the virtual memory for the elastic stack to run properly command used is sysctl -w vm.max_map_count=262144, this gives elastic stack about 2.6 gbs of ram to ensure it runs efficiently)
- (Final task is downloading and launching docker elk container, includes name, image and published ports)   
 
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
[screenshot of docker ps output](blob/master/Images/docker_ps.png.png)
 
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-List the IP addresses of the machines you are monitoring (40.112.185.41, 138.91.189.25)
 
We have installed the following Beats on these machines:
- Specify which Beats you successfully installed. (filebeats)
 
These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc. (filebeats monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.)
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
 
SSH into the control node and follow the steps below:
- Copy the (elkserverconfig) file to (the new VM/container)
- Update the (hosts) file to include the (elkserver IP address) 
- Run the playbook, and navigate to (elkserver VM) to check that the installation worked as expected by running sudo docker ps. 
 
-Answer the following questions to fill in the blanks:_
- Which file is the playbook? (/etc/ansible/roles/filebeat-playbook.yml) Where do you copy it? (Elkserver VM)
- Which file do you update to make Ansible run the playbook on a specific machine? (etc/ansible/hosts) How do I specify which machine to install the ELK server on versus which to install Filebeat on? (the IP is listed under the group in the hosts file and the playbook mentions the group to apply to all IPs within the group.) 
-Which URL do you navigate to in order to check that the ELK server is running?
(http://52.240.59.170:5601)
 
 
