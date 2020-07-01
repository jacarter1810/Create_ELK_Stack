## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
Diagrams/Network_Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.
Ansible/ansible.cfg

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly fault tolerant, in addition to restricting access/traffic to the network.

Load balancers protect availability of the network by preventing overloading of the system.
The jump box limits access to the network, by acting as a protected gateway available through ssh.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

Filebeat will forward new log events.

- _TODO: What does Metricbeat record?
Metricbeat will collect metrics and system service information

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name           | Function                | IP Address                                              | Operating System |
|----------|----------|------------|------------------|
| Jump Box    |  Gateway                | Private 10.0.0.4 Public 138.91.196.133               | Linux       |
| DVWA VM1|  Webserver             | Private 10.0.0.5 Public 104.42.58.36         | Linux       |
| DVWA VM2|  Webserver             | Private 10.0.0.6 Public 104.42.58.36         | Linux       |
| ELK Stack   |  Security                 | 52.151.55.172                                         | Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses
SSH from local machine
Local Machine IP

Machines within the network can only be accessed by the Jump Box Provisioner
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?

Jump Box 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No, SSH Accessible | 10.0.0.4    |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?

Ansible guarantees that the same configuration is applied to all machines.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker
- Install pip
-Install Python
-Increase Virtual Memory
-Download and launch elk container
-List ports on which ELK can run

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Image:
Ansible/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

DVWA VM1 10.0.0.5
DVWA VM2 10.0.0.6


We have installed the following Beats on these machines:
FileBeat
MetricBeat

These Beats allow us to collect the following information from each machine:
Filebeat will collect log events and forward them to Logstash, while Metricbeat will collect system metrics, like a given amount of inbound and outbound traffic over a given period of time.

Creating a Cloud Environment

Sign up for Azure account

Login
From the Home click on Resource Group

Create a Resource Group 

Resource Group - a collection of resources grouped together for the setup
IE. Sales, Customer Service, etc.

Resource Group Created - RedTeamWest

Select Region: (US) West US
 Alt: (US) West US 2

Create a Virtual Network

Find Virtual Networks in Azure and select Add
Assign to resource group: RedTeamWest
Name of Virtual Network: VNWest
Select Region: (US) West US
Select IP Addresses: 10.0.0.0/16

Note: You can also make smaller networks by changing cider notation.
10.0.0.0/8 IP addresses: 10.0.0.0 – 10.255.255.255
10.0.0.0/16 IP addresses: 10.0.0.0 – 10.0.255.255
172.16.0.0/12 IP addresses: 172.16.0.0 – 172.31.255.255
192.168.0.0/16 IP addresses: 192.168.0.0 – 192.168.255.255
192.168.1.0/24 IP addresses: 192.168.1.0 – 192.168.1.255
Subnet: Default

Create a Network Security Group (NSG)

Acts as a basic firewall
Use NSG to block and allow traffic to/from/within virtual network 

Find Network Security Group in Azure and select Add

Select Resource Group: RedTeamWest
Name of Virtual Machine: DVWA VM 1
Select Region: (US) West US



Create a Virtual Machine to Place on the Virtual Network

(Update: Azure now allows you to create SSH keys directly in the portal environment as you are creating your VM)

Note: We will be using SSH to authenticate into the VM, therefore we need to create an ssh key pair, which we can do in Git Bash.

In Git Bash
ssh-keygen	(creates a public and private key pair)

Key pair will be saved on local machine
Private Key: /Users/UserName/.ssh/id_rsa
Public Key: /Users/UserName/.ssh/id_rsa.pub
Display Public Key from Bash Run - cat /Users/UserName/.ssh/id_rsa.pub
Copy the public key and paste into the appropriate Azure window


Find Virtual Machines in Azure and select Add

Select Resource Group: RedTeamWest
Name of Virtual Machine: JumpBoxProvisioner
Select Region: (US) West US
Select Availability Options: Default
Select Image: Ubuntu Server 18.04 LTS
Select VM Size: Depends on demand
Select Authentication Type: SSH or Password
Note: VM can be accessed from any IP, but this can be changed in network settings
Selected: SSH
Create User Name: RedTeamAdmin
Select Inbound Ports: SSH (22)

The rest of the setup was default settings.

IP Addresses
Static Public IP address: 40.78.90.86
Private IP address: 10.0.0.4









SSH into the VM

Open Git Bash or Command line
Run:
ssh RedTeamAdmin@40.78.90.86



Install Docker on Jump Box

sudo apt-get update				(Make sure system is up to date)
sudo apt install docker.io			(Install Docker on VM)
sudo docker pull ubuntu			(grab Ubuntu image from Docker)
sudo docker run -ti ubuntu bash		(-ti makes it terminal interactive)

Setup and Launch a Docker Container Running Ansible
 
sudo systemctl status docker		(Check if Docker is running)
sudo systemctl start docker			(This will start Docker if it was not running)
sudo docker pull cyberxsecurity/ansible	(Pull Ansible container
sudo docker run -ti cyberxsecurity/ansible bash	(Launch Ansible container)
sudo docker container list -a			(list all containers)

sudo docker ps				(shows containers currently running)

sudo docker start ContainerName		(Start the container upbeat_germain)

sudo docker attach ContainerName	(Attach container upbeat_germain)

Looks like:
RedTeamAdmin@Jump-Box-Provisioner:~$ sudo docker attach upbeat_germain
root@4cce4b6093c1:~#
 
You are now inside the ansible container
 
 
 
 
 
 


 
Note: We want the new VM to be accessible only by the Ansible Container, and the most secure way to do that is using an SSH key.  The following commands are run in the Ansible container through the terminal to create and share the SSH key.
 
From Ansible Container Terminal:
ssh-keygen	(creates a public and private key pair on VM)

Key pair will be saved on the Ansible Container
Private Key: /root/.ssh/id_rsa
Public Key: /root/.ssh/id_rsa.pub
Display Public Key from Bash Run - cat /root/.ssh/id_rsa.pub

Begin creating the new VM in the Azure Environment
Copy the public key and paste into the appropriate Azure window
 
Create a New VM Acting as a Webserver
 
Find Virtual Machines in Azure and select Add

Select Resource Group: RedTeamWest
Name of Virtual Machine: DVWA-VM1
Select Region: (US) West US
Select Availability Options: Availability Set -> Create New -> RedTeamAS
Select Image: Ubuntu Server 18.04 LTS
Select VM Size: Depends on demand
Select Authentication Type: SSH or Password
Selected: SSH
Paste SSH public key generated by Ansible Container
Create User Name: RedTeamAdmin
Select Inbound Ports: SSH (22)

The rest of the setup was default settings.

IP Addresses
Static Public IP address: 104.42.58.36
Private IP address: 10.0.0.5
 
Repeat Steps for a second VM, DVWA-VM2




Back in the Ansible Container
 
Check for connectivity to the newly created VM
Run
ping 10.0.0.5			(This will help you determine if the server is up)

 
 
exit		(end ssh session)

 
From Ansible Container
If server is up:
Edit the Ansible Config File	(/etc/ansible/ansible.cfg)
nano /etc/ansible/ansible.cfg

Remove the hash(#) in front of remote_user
Change root to your new login name 	(AnsAdmin)

Save changes ctrl+O Enter, then Exit ctrl+X

Edit the Ansible Hosts File
nano etc/ansible/hosts

Remove the hash(#) in front of [webservers]
Add the private IP’s of DVWA-VM1 to the webservers section



ansible -m ping all 				(Test container’s connectivity)

(note: ELK Server is created but not upland running, however there is success to both DVWA Servers)

Use a YAML Playbook and Ansible Provisioner to Automate the Setup of VM

Create a YAML playbook
nano /etc/ansible/DVWA_Setup.yml
Paste code from DVWA_Setup file from local machine into DVWA_Setup.yml to Ansible container (Create_ELK_Stack/Ansible/DVWA_Setup.yml)

Run Playbook
ansible-playbook /etc/ansible/DVWA_Setup.yml	
(This will run a series of installs on the DVWA-VM1 Server to get it up.)

Use Browser to Navigate to Server



SSH into DVWA-VM1 from the Ansible Container in order to make sure that it’s running.
ssh AnsAdmin@10.0.0.5	(The remote user from the ansible.cfg file)
 

 
When you are in run:
curl localhost/setup.php			(HTML code for server should show up)


Adding a Load Balancer 


Find Load Balancer in Azure and select Add

Select Resource Group: RedTeamWest
Name of Virtual Machine: LBWest
Select Region: (US) West US
IP: Static

Add a health probe by going to the Load Balancer and on the left hand side selecting health probe.

Name: HealthProbeWest
Protocol: TCP
Port: 80
Interval: 5 seconds
Unhealthy Threshold: 2 consecutive failures

Add a Backend Pool by going to the Load Balancer and on the left hand side selecting Backend Pool

Name: PoolWest
Virtual Network: VNWest (RedTeamWest)
Associated to: Virtual Machines
Add the DVWA-VM1 to the load balancer backend pool

Create a second DVWA VM for Redundancy

The second VM will use the same IP address as the first so that if one goes down, the site will still remain active.  Meanwhile the load balancer will determine which server is visited by the client.

Follow the same steps used to create the first DVWA Server
Name: DVWA-VM2
Use the same SSH key (stored in the Ansible Container)
Add the new VM’s private IP to the Ansible Hosts file
Run the Ansible DVWA_Setup file
Ping and Curl the new machine to check that it is up and running

Add the second DVWA Server to the backend pool of the load balancer



Create a New VM to Run ELK

Find Virtual Machines in Azure and select Add

Select Resource Group: RedTeamWest
Name of Virtual Machine: ELK-Stack
Select Region: (US) West US
Select Availability Options: Availability Set -> Create New -> RedTeamAS
Select Image: Ubuntu Server 18.04 LTS
Select VM Size: Depends on demand
Select Authentication Type: SSH or Password
Selected: SSH
Paste SSH public key generated by Ansible Container
Create User Name: AnsAdmin
Select Inbound Ports: SSH (22)

The rest of the setup was default settings.

IP Addresses
Public IP address: 168.61.67.41
Private IP address: 10.0.0.7

Edit the Ansible Hosts File
nano etc/ansible/hosts
Remove the hash(#) in front of [elkservers]
Add the private IP’s of the networks elkservers



Create the ELK PLaybook
Before continuing you must change the inbound security rules of the network security gruop in azure.  Allow inbound traffic on ports 5601 and 9200.  These are the ports used to communicate with the elk machine



Copy the contents of the elk playbook from Create_ELK_Stack/Ansible/elk-playbook
into the file Ansible Container /etc/ansible/roles/elk-playbook

Run the Playbook
Ansible-playbook etc/ansible/roles/elk-playbook.yml


SSH into ELK-Stack
ssh AnsAdmin@10.0.0.7

Inside the ELK-Stack VM run:
sudo docker start elk
sudo docker ps



sudo docker attach elk



When ELK is up and running you should be able to access it through your web browser.
Example with my IP
http://168.61.67.41:5601/app/kibana#/home





Installing Filebeat and Metricbeat on ELK-Stack

You will need to create a filebeat configuration file on the Ansible Container
/etc/ansible/files/filebeat.yml
Open the provided file Create_ELK_Stack/Ansible/filebeat-configuration
(note: you might want to open this file in a text editor with numbered lines such as notepad++)
Scroll to line #1106 and change the IP to the IP of your ELK machine
Copy and Paste the contents into the file into /etc/ansible/files/filebeat.yml


A version of the playbook can be found in Create_ELK_Stack/Ansible/filebeat-playbook
Copy and paste the contents into a file /etc/ansible/roles/filebeat-playbook.yml
Run the playbook:
ansible-playbook filebeat-playbook



Navigate back to the ELK-Stack home page
http://52.151.55.172:5601
Click Add Log Data
Select System Logs
Select the DEB tab under Getting Started
(This will provide the most up to date steps for the Filebeat playbook)
Scroll to the bottom of the page and click “check data”

Filebeat page before logs are transferred.




Filebeat page after logs are successfully transferred


Follow the similar steps for Metricbeat setup

Navigate back to the ELK-Stack home page
http://52.151.55.172:5601
Click Add Metric Data
Select Docker Metrics
Select the DEB tab under Getting Started
(This will provide the most up to date steps for the Filebeat playbook)
Scroll to the bottom of the page and click “check data”






Metricbeat page after metrics are successfully transferred


