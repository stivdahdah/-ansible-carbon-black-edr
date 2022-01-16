# Ansible Playbook for VMware Carbon Black EDR Installation

No Galaxy modules are required.

Playbook file: carbon_edr_installation.yml

This playbook will help you to install Carbon Black EDR on RHEL/CentOS.

This playbook has 3 tasks: <br>
Task-01: Create a directory called CarbonBlackApp in /opt <br>
Task-02: Download and Extract VMware Carbon EDR from the github repositary <br>
Task-03: Install VMware Carbon Black EDR Control from the directory /opt/CarbonBlackEdr/

Requirements:
- The network connection between your node and Github should be allowed since this playbook will fetch the installation from the CB server directly.

Notes:
You can change the src to be pointed to a local host.


**Example Playbook**


```
---


- name: Playbook to Download and Install VMware Carbon Black EDR 
  hosts: all
  
  tasks:
  - name: Create a Directory called CarbinBlackEDR in opt
    become: yes
    file:
      path: "/opt/CarbonBlackEdr"
      state: directory
      mode: 0755

  - name : Download and Extract VMware Carbon Black EDR Control
    become: yes
    unarchive:
      src: "https://github.com/stivdahdah/ITEDTAFAGWq1231/raw/main/CarbonBlackLinuxInstaller-v7-0-3-15300.tar.gz"
      dest: "/opt/CarbonBlackEdr/"
      mode: 0755
      remote_src: yes

  - name: Install VMware Carbon Black EDR
    become: yes
    shell:
      "./CarbonBlackClientSetup-linux-v7.0.3.15300.sh"
    args:
        chdir: "/opt/CarbonBlackEdr/" 
    register: output
```
