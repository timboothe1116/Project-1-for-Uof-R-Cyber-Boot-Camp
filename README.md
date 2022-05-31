# Project-1-for-Uof-R-Cyber-Boot-Camp
this repository will provide details and example for how I completed Project 1 for the Boot Camp. 
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/timboothe1116/Project-1-for-Uof-R-Cyber-Boot-Camp/blob/main/Azure%20ELK%20Project.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/timboothe1116/Project-1-for-Uof-R-Cyber-Boot-Camp/blob/main/Ansible/beats-playbook.yml

https://github.com/timboothe1116/Project-1-for-Uof-R-Cyber-Boot-Camp/blob/main/Ansible/dvwa-playbook.yml


https://github.com/timboothe1116/Project-1-for-Uof-R-Cyber-Boot-Camp/blob/main/Ansible/elk-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_
-Load balancers provide protection against DOS by analyzing incoming traffic and sends to appropriate server. This helps to prevent the servers from being overloaded with traffic. Load balancers will divert traffic from a server that may not be working properly. A jump box will limit the public access to virtual networks. Private IP addresses are needed to access other virtual machines. A jump box serves as a monitor/control of the access to virtual networks and all that goes with it. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
-What does Filebeat watch for?
-Filebeat generates and organizes log files and will adjust for changes.

-What does Metricbeat record?
-Metribeat monitors the metrics from the OS and maintains the services available on the server. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function                   | IP Address | Operating System |
|----------|----------                  |------------|------------------|
|Jump Box  | Gateway & Docker w/ Ansible| 10.7.0.4   | Linux Ubuntu     |
| Web1     | Web Server used to run DVWA| 10.7.0.5   | Linux Ubuntu     |
| Web2     | Web Server used to run DVWA| 10.7.0.6   | Linux Ubuntu     | 
| Elkvm    | Run ELK Container & Kibana | 10.8.0.4   | Linux Ubuntu     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-174.216.176.4 (My Public IP)

Machines within the network can only be accessed by Jump Box VM.
-Which machine did you allow to access your ELK VM? Jump Box VM
         What was its IP address? 40.86.30.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.7.0.5 10.7.0.6    |
| Web1     | No                  | 10.7.0.4             |
| Web2     | No                  | 10.7.0.4             |
| Elk VM   | Yes (Port 22)       | 10.7.0.5 10.7.0.6    |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible? It streamlines the process by not having to manually configure ELK. It also oversaw with control what was being installed on the machine.

The playbook implements the following tasks:
-The first task of the elk playbook installs docker.io on the Elk virtual machine
-Downloads, installs and executes the docker elk container on the Elk vm on restart so the elk container doesn't need to be manually started
-Elk requires more virtual memory so this task increases the memory to 262144

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web1: 10.7.0.5 Web2: 10.7.0.6
We have installed the following Beats on these machines:
Filebeat and Metricbeat
These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects log information and specifies which file has been changed and was it either changed to Elasticsearch or Logstash. If you connect to Kibana you can see the Filebeat’s output and see logs that may have been changed over a certain time period. Metricbeat displays information for all processes being ran on the system to include file system, CPU usage, memory. If you connect through Kibana you can select any of the above mentioned as see the metrics of such request.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the  file to include...
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Filebeat-playbook.yml Where do you copy it?_ /etc/ansible/roles/filebeat.playbook.yml
-Which file do you update to make Ansible run the playbook on a specific machine? Filebeat-config.yml  
How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
