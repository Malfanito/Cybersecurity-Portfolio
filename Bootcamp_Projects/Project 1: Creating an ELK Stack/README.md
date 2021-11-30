## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/Malfanito/ELK-Stack/blob/main/Diagrams/ELK%20Stack%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. The installed health probe will also ensure high availablity and visability on any down servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system changes.

The configuration details of each machine may be found below.

| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump-Box-Provisioner | Gateway    | 10.0.0.7   | Linux (Ubuntu)   |
| Web-1                | DVWA       | 10.0.0.5   | Linux (Ubuntu)   |
| Web-2                | DVWA       | 10.0.0.6   | Linux (Ubuntu)   |
| Purp_Elk_1           | ELK Stack  | 10.1.0.5   | Linux (Ubuntu)   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- My public IP

Machines within the network can only be accessed by Jump-Box-Provisioner (10.0.0.7).

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner | Yes                 | My Public IP         |
| Web-1                | No                  | 10.0.0.7             |
| Web-2                | No                  | 10.0.0.7             |
| Purp-ELK-1           | Yes                 | My Public IP         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it makes the installation of applications streamlined in my virtual machines. This also helps if I am ever interested in scaling up the infrastructure (future-proofing). 

The playbook implements the following tasks:
- Installs Docker
- Installs Python3
- Increase Virtual Memory
- Install ELK in a docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/Malfanito/ELK-Stack/blob/main/Images/docker%20ps%20on%20elk.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web1)
- 10.0.0.6 (Web2)

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Log Data and Traffic Data
- Changes to file structure and access attempts

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the files to /etc/ansible/.
  - `git clone https://github.com/Malfanito/ELK-Stack`
  - `cp -r ./Elk-Stack/Ansible /etc/ansible`
  - You will have to edit the config files for metricbeat and filebeat to represent your private IPs.
- Update the hosts file to include the private IP address of the new machine as an Elk server.
  - Add [host name] to the bottom of the hosts file
  - Underneath that, add the private IP(s) of the machines. (Note: if using more than one machine, use a new line for each IP)
- Run the playbooks, and navigate to http://[publicIP]:5601/app/kibana to check that the installation worked as expected.
  -  To run the playbook, run the following command while in the /etc/ansible directory:
    - `ansible-playbook [playbookfile.yml]`
