## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

Image File in Draw.io:
https://app.diagrams.net/#G1lFBNNnV-qYdNJpSXesKTfW3OjQ3XAqp7

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Load balancers protect availability of the network by preventing overloading of the system.
The jump box limits access to the network, by acting as a protected gateway available through ssh.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- _TODO: What does Filebeat watch for?
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

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

Ansible/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

DVWA VM1 10.0.0.5
DVWA VM2 10.0.0.6


We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed

FileBeat
MetricBeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat will collect log events and forward them to Logstash, while Metricbeat will collect system metrics, like a given amount of inbound and outbound traffic over a given period of time.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to Ansible container
- Update the hosts file to include the ELK Server IP
- Run the playbook, and navigate to the IP of the ELK Stack server to check that the installation worked as expected.
