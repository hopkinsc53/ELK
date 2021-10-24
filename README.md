README.md

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansibledocker-scripts/ansible.cfg file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/hopkinsc53/GTechcybersecurity2021/blob/f2eaeb03ae42d555194fc08ac4e28b6dc52ba7bc/Ansibledocker-scripts/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting denial of service to the network.
- Load balancers protect the Availability aspect of the CIA triad of cybersecurity 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system system files.
- Filebeat watches log files, collects log events and sends them to Elasticsearch for indexing. 
- Metricbeat records the operating system and it's services then sends them to Eelasticsearch.  

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System   |
|----------|----------|------------|--------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux/Ubuntu 18.04 |
| OffSec1  | server 1 | 10.1.0.6   | Linux/Ubuntu 18.04 |
| OffSec2  | server 2 | 10.1.0.7   | Linux/Ubuntu 18.04 |
| OffSec3  | server 3 | 10.1.0.8   | Linux/Ubuntu 18.04 |
| ELK      | Monitor  | 10.2.0.4   | Linux/Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.202.170.58

Machines within the network can only be accessed by my local workstation .
- 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.202.170.68        |
| OffSec1  | No                  | 10.0.0.1             |
| OffSec2  | No                  | 10.1.0.1             |
| OffSec3  | No                  | 10.1.0.1             |
| ELK      | NO                  | 10.0.0.2             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with ansible is the ability to update multiple devices at the same time; Where as, one would have to update every single system individually. In networks with many systems connected this could prove to be very time consuming. 

The playbook implements the following tasks:
- Installs Docker.io
- Installs pip3 and Python Docker Module
- Downloads and launches the ELK container alloting appropriate ports
- Allows ELK to run every reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Filexfer_dockertojump](https://user-images.githubusercontent.com/77931754/138440140-e059a8c3-b4ed-4977-95d6-459dd733ead9.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- The web servers with internal network IP addresses of 10.1.0.6, 10.1.0.7, 10.1.0.8

We have installed the following Beats on these machines:
- On the webservers OffSec1, OffSec2, OffSec3

These Beats allow us to collect the following information from each machine:
- Filebeat records log data which allows one to monitor device traffic
- Metricbeat records hardware data such as OS info, CPU and memory usage, ect.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Deployment-playbook.yml file to /etc/ansible/roles
- Update the /etc/ansible/hosts file to include the IP addresses in the web server and ELK groups. Uncomment the web servers portion and add the ELK portion for it to work 
- Run the playbook, and navigate to 52.188.120.165:5601/app/kibana to check that the installation worked as expected.
