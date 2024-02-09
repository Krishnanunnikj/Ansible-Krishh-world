To install and configure Ansible on Ubuntu
Create 3 instances 2 slaves and 1 master
install Ansible on the master instance with the help of ansible docs "https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html"
Now create a keygen using the below command
ssh-keygen
Then cd to .ssh folder
Then Copy the id_rsa_pub data
And then copy it on all the slaves under cd .ssh/ Authorised keys
Then On the Master machine got cd /etc/ansible/
Edit hosts and add private IPs of all the slave machines
You can group them using [slave 1] and [slave 2]
Once done ping the slave using the below commands
ansible -m ping all
Now we have to create a playbook
sudo nano playbook1.yaml
#####################################################
---
- name: Installing Java on slave1
  hosts: Slave1
  become: yes
  tasks:
   - name: Installing Java          
     apt: name=openjdk-17-jdk state=latest update_cache=yes 
- name: Installing Mysql on slave2
  hosts: Slave2
  become: yes
  tasks:
   - name: Installing Mysql
     apt: name=mysql-server state=latest update_cache=yes

**######################################################**

Now run the commad 
ansible-playbook playbook1.yaml

 
