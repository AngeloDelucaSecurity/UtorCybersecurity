## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![Untitled Diagram drawio](https://user-images.githubusercontent.com/96212470/146653256-6d81fe39-3d7e-4251-ac24-b96ac66132dd.png)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound connections to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load Balancers are used to increase capacity and can mitigate DDOS attacks

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs viewable on kibana.
Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function    | IP Address    | Operating System |
|----------|-------------|---------------|------------------|
| Jump Box | Gateway     | 10.0.0.4      | Linux            |
| Web-1    | Web Server  | 10.0.0.5      | Linux            |
| Web-2    | Web Server  | 10.0.0.6      | Linux            |
| ELK      | Elk Server  | 104.43.227.46 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
99.246.131.0/24 

Machines within the network can only be accessed by the authorized user who has access to the jump box, access provided by ssh keypair.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
99.246.131.0/24 on port 5601 (firewall rule)
10.0.0.4 (ssh keys)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 99.246.131.0/24      |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELK      | Yes                 | 99.246.131.0/24      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Creating ansible scripts is highly configureable as you can set whatever is needed to be installed and it makes installing and creating new devices 
simple and easy. Create a YAML script with the applications specified and lauch them to a new device. Instead of installing each package individually 

The playbook implements the following tasks:
- Install Docker.io
- Install python-pip3
- Install Docker Module
- Download and launch container
- Enable the service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![first](https://user-images.githubusercontent.com/96212470/146652728-2ff7bdca-2ab4-443d-a624-d51638dfcce8.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 
- 10.0.0.5 Web-1
- 10.0.0.6 Web-2

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat Captures system logs created by Web-1 and Web-2
- Metricbeat Captures logs from docker by default it captures: container, cpu, diskio, healthcheck, info, memory and network

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
```
curl -o elk.yml https://github.com/AngeloDelucaSecurity/UtorCybersecurity/tree/main/ansible/elk.yml

```

- Update the host file for anisbible to include:

![second](https://user-images.githubusercontent.com/96212470/146652709-de90337a-e352-4ddf-a345-01aa08167752.PNG)


- Run the playbook, with the command:
```
 ansible-playbook elk.yml
```
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- Update the hosts file
- Navigate to 20.124.245.16:5601/app/kibana


