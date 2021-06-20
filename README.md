## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Network Diagram in Diagrams/AzureNetworkDiagram.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

  - Elk.yml, filebeat-playbook.yml, metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting DDoS Attacks to the network. Load Balancers protect the availability of a network. The advantage of a jump box is that it is a hardened monitoring device that spans two dissimilar security zones and provides a controlled means of access between them.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Jumpbox and system network. Filebeat monitors the logfiles and metricbeat records metrics from the operating system and services.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web1     | DVWA     | 10.0.0.5   | Linux            |
| Web2     | DVWA     | 10.0.0.6   | Linux            |
| Web3     | DVWA     | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 199.83.221.185

Machines within the network can only be accessed by SSH. The jumpbox provisioner also can access the ELK VM (104.42.195.37)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 199.83.221.185       |
| ELK      | No                  | 104.42.195.37        |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it was done with a configuration file, which can be easily modifed or used again to recreate the configuration.

The playbook implements the following tasks:
- Installs docker.io
- Installs python3-pip
- Installs Docker Module
- Uses more memory
- Downloads and launches a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

```bash
root@6160a9be360e:/etc/ansible# ansible-playbook elk.yml
PLAY [Configure Elk VM with Docker] ****************************************************
TASK [Gathering Facts] *****************************************************************
ok: [10.1.0.4]
TASK [Install docker.io] ***************************************************************
changed: [10.1.0.4]
TASK [Install python3-pip] *************************************************************
changed: [10.1.0.4]
TASK [Install Docker module] ***********************************************************
changed: [10.1.0.4]
TASK [Increase virtual memory] *********************************************************
changed: [10.1.0.4]
TASK [Increase virtual memory on restart] **********************************************
changed: [10.1.0.4]
TASK [download and launch a docker elk container] **************************************
changed: [10.1.0.4]
TASK [Enable service docker on boot] **************************************
changed: [10.1.0.4]
PLAY RECAP *****************************************************************************
10.1.0.4                   : ok=1    changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6
10.0.0.7

We have installed the following Beats on these machines:
10.0.0.5
10.0.0.6
10.0.0.7

These Beats allow us to collect the following information from each machine:
syslogs - These allow us to see how the machine has been used including the components of the VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to the docker container.
- Update the hosts file to include all the intended vm IP addresses
- Run the playbook, and navigate to kibana to check that the installation worked as expected.

The playbook files are the ones that end with -playbook.yml and you can update the hosts file to make ansible run the playbook on a specific machine. You have to visit http://[VM.IP]:5601/app/kibana in order to see if the instalation was successful 
