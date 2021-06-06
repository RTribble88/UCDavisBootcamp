## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(https://drive.google.com/file/d/1tAHVnUs7bq6HG2IWb8bSuBIclOd14s5W/view?usp=sharing)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

```
---
- name: Installing and Launch Filebeat
  hosts: webservers
  become: yes
  tasks:
    # Use command module
  - name: Download filebeat .deb file
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb

    # Use command module
  - name: Install filebeat .deb
    command: dpkg -i filebeat-7.4.0-amd64.deb

    # Use copy module
  - name: Drop in filebeat.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml

    # Use command module
  - name: Enable and Configure System Module
    command: filebeat modules enable system
   # Use copy module
  - name: Drop in filebeat.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml

    # Use command module
  - name: Enable and Configure System Module
    command: filebeat modules enable system

    # Use command module
  - name: Setup filebeat
    command: filebeat setup

    # Use command module
  - name: Start filebeat service
    command: service filebeat start

    # Use systemd module
  - name: Enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes
```


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect? 

Load balancers protect the availaboloty of the machine.

What is the advantage of a jump box? 

A jump box birdges two diffrent security zones and controls access between them. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system Metrics.

What does Filebeat watch for? 

File beat monitors log files and collects log events.

What does Metricbeat record? 

Merticbeat collects syetem metircs from the system operating system and running services. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.9   | Linux            |
| Web-2    | Server   | 10.0.0.10  | Linux            |
| Elk      | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

73.235.128.52

Machines within the network can only be accessed by the Jumpbox.

Which machine did you allow to access your ELK VM? What was its IP address?

I allowed StargatePortal access to the ELK VM its Ip is 23.101.204.96

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.235.128.52        |
| Web-1    | No                  | 23.101.204.96        |
| Web-2    | No                  | 23.101.204.96        |
| ELK      | Yes                 | 73.325.128.52        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

Automating with ansibles takes mundane tasks away from the Administrtor and allows them to focus on other things.

The playbook implements the following tasks:

.Install Filebeat

.Copy pre confgiured image of filebeat

.Setup the pre-configured image of filebeat

.Start Filebeat

.Enable filebeat on boot


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://docs.google.com/document/d/1oEA14mSlV8Gzt4HDuNzwxqkWynhnPIUuljWfh-MgQrM/edit?usp=sharing)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

10.0.0.9

10.0.0.10

We have installed the following Beats on these machines:

Filebeat

Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-install.yml file to your files directory.
- Update the filebeat-config.yml file to include your Elk Server IP
- Run the playbook, and navigate to your Elk Staks IP to check that the installation worked as expected.


****
