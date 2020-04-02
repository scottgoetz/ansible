# ansible
Ansible is a "software provisioning, configuration management, and application-deployment tool."  It runs on a Unix system, and can be used to manage Unix and Windows systems. Ansible is only installed on the Server system, it does not install Ansible agents on the client/target systems.

Python 2.7 is required to be installed on the client/target:
* apt-get install python -y

Reference this article when following the next steps:  https://www.linode.com/docs/applications/configuration-management/running-ansible-playbooks/

**Configure A records for primary domain and subdomains before running these scripts. The domains need to be established in DNS in order for letsencrypt to obtain SSL certs**

These instructions are to be implemented on your Ansible Server:
* sudo apt install ansible
* sudo apt install whois
* Generate a password hash for the new unpriv user, annotate hash for use in .yml files:
  * or mkpasswd -m sha-512
* Disable host key checking:
  * sudo vi /etc/ansible/ansible.cfg
* Add Client hostnames and IPs to Ansible "hosts" file:
  * sudo vi /etc/ansible/hosts 
  * Refer to ansible scripts for default names: i.e. mail, core, redirector, drone
* sudo apt-get install sshpass
* Generate ssh keypairs for Clients, annotate paths for .yml files:
  * ssh-keygen
* Modify variables in the "vars" section of each Ansible script. Data that needs to be modified is contained between angle brackets (e.g. <variable_name>) need to be modified.
* Make sure to change Hostname on VPS

Execution:
* Run initial secureSetup.yml Ansible script to configure Clients in a secure state:
  * sudo ansible-playbook --ask-pass -u root secureSetup.yml
* Run secondary Ansible scripts to configure Client for various purposes:
  * sudo ansible-playbook -u <unprivileged_user_name> <script_name>.yml --key-file /home/<ansibleServer_username>/.ssh/id_rsa --ask-become-pass
  
SSH with public keys:
  * ssh USER@IP -i ~/.ssh/id_rsa
  
For when you rebuild a Client and need to delete old keys:
  * sudo ssh-keygen -f "/root/.ssh/known_hosts" -R clientIp

How to setup GoPhish infrastructure:
 1. Run secureSetup.yml on Core Server (server that GoPhish is installed on), Web Redirector, and Mail Server
 2. Run redirectorSetup.yml on Web Redirector
 3. Run postfix_*.yml on Mail Server
 4. Run GoPhish.yml/GhostPhish.yml on Core
