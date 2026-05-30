# SonarQube Installation using Ansible

## Project Overview

This project automates the installation and configuration of SonarQube on Ubuntu using Ansible.

Real IP addresses, passwords, and private lab details are not included. Replace placeholders before running.

## Project Structure

```text
SonarQube-Install/
├── inventory.ini
├── install-sonarqube.yml
└── README.md

Features
Installs Java
Installs PostgreSQL
Creates SonarQube database
Creates SonarQube Linux user
Downloads and installs SonarQube
Configures SonarQube as a systemd service
Enables SonarQube auto-start
Prepares SonarQube for Jenkins integration

SonarQube ZIP installs require a supported Java runtime, and current SonarQube Server docs list Java 21 for ZIP-based server installs. SonarQube also recommends PostgreSQL instead of the embedded H2 database for non-test usage.

Run command

Install PostgreSQL collection first:

ansible-galaxy collection install community.postgresql

Then run:

ansible -i inventory.ini sonarqube -m ping
ansible-playbook -i inventory.ini install-sonarqube.yml


Features
Installs Java
Installs PostgreSQL
Creates SonarQube database
Creates SonarQube Linux user
Downloads and installs SonarQube
Configures SonarQube as a systemd service
Enables SonarQube auto-start


Prepares SonarQube for Jenkins integration
Inventory Example
[sonarqube]
sonarqube-01 ansible_host=<SONARQUBE_IP>

[sonarqube:vars]
ansible_user=<SSH_USER>
ansible_become=true
Placeholders to Update
Placeholder	Description
<SONARQUBE_IP>	SonarQube server IP address
<SSH_USER>	SSH username for Ubuntu VM

Verify Connectivity
    ansible -i inventory.ini sonarqube -m ping

Expected:

        pong

Install Required Ansible Collection
    ansible-galaxy collection install community.postgresql
Run Installation
    ansible-playbook -i inventory.ini install-sonarqube.yml
Verify Service
    ansible -i inventory.ini sonarqube -m shell -a "systemctl status sonarqube --no-pager"

Access SonarQube
    http://<SONARQUBE_IP>:9000

Default login:

    Username: admin
    Password: admin