# ansible.yml_file
Has ansible playbooks we made for our project. Includes playbooks for Elk server, filebeat, and metricbeat. It also includes two networking diagrams,
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

~/ansible.yml_file/Diagrams/Network_Diagram_ELK_VM

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly <available and reliable>, in addition to restricting <unauthorized visitors> to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load Balancers protect the availiblity aspect of the CIA triad. Load balancers protect servers from being flooded with traffic, which limits data availability.
Jump box gives us the advantage of being our access point to our Virtual Machines, as opposed to loggin into each server individually. We can also use our jump box to set up a provisioner like ansible. 
Provisioners are important because we can update our VM's and Web VM's by running ansible-playbooks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
A filebeat watches for log files from specific files. 
- _TODO: What does Metricbeat record?_
Metricbeat records machine metric such as Uptime and Cpu usage.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|   Name   |       Function       | IP Address | Operating System |   
|:--------:|:--------------------:|:----------:|:----------------:|
| Jump Box |        Gateway       |  10.0.0.1  |       Linux      |   
|   Web-1  |   Server/container   |  10.0.0.6  |       Linux      |   
|   Web-2  |   Server/container   |  10.0.0.8  |       Linux      |  
|   Web-3  |   Server/container   |  10.0.0.9  |       Linux      |  
|   Elk    | Server/Elk container |  10.1.0.4  |       Linux      |  

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the <Jump box> machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
72.197.56.27

Machines within the network can only be accessed by <SSH connection>.
I allowed ssh connection to all machines in network. HTTP access to backend pool. And all these are accessible via 	
72.197.56.27

A summary of the access policies in place can be found in the table below.

|       Name      | Publicly Accesible | Allowed IP Addresses  |
|:---------------:|:------------------:|:---------------------:| 
|     Jump Box    |         Yes        |      72.197.56.27     |
| DWVA Containers |         no         |          ANY          |
|       Elk       |         no         |      72.197.56.27     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
 <The main advantage is that we don't have to login to ever server and configure each one individually. This is advantageous because it reduces user error and it guarantees parity amongst all configured VMs.>
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- first we had to download and install docker
- then we had to allow our machine more memory to run Docker
- once we did that we had to download and install a docker container within our Elk vm
- We also had to enable the service, so we added that to the playbook.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
<10.0.0.6 10.0.0.8 10.0.0.9>
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
<Succefully installed meatricbeat and filebeat.>
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
<Filebeat collects log files from specific files such as logs from Apache. From Apache log files I would expect to see errorlogs. These error logs document any issues it encounter when apache was processesing http requests. Metricbeat collects the computer metrics. We would see a CPU metrics that record how the CPU resources have been distrubuted throught different sessions.> 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the  filebeatconfig.yaml file to webserver's  filebeat directory.
- Update the yaml file to include whatever you need.
- Run the playbook, and navigate to <Web1 server> to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
The file is the elkplaybook.yml. I would copy it in the ansible docker. 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
YOu would have to update the hosts file. In order to specifiy, you would have to create an [Elk server] field and indicate in playbook which host you are installing program on.
- _Which URL do you navigate to in order to check that the ELK server is running?
http://[ElkserverpublicIP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
