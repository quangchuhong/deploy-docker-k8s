# Ansible-docker-k8s-iptalbes
Triển khai hệ thống docker-k8s

# Cấu Trúc triển khai 
- Roles: docker-k8s-iptables

- OS: Triển khai trên hai hệ điều hành Ubuntu16.04 vs CentOS 7.

- Site.yml: File run install Roles.

- File hosts: List ip server

- Template: firewall.bash.j2, iptables.sh

# Run Ansibles:

- ansible-playbook -i hosts site.yml

- ansible-playbook -i hosts site.yml --user quangch --ask-pass

- ansible -i hosts -m ping all

- ansible-playbook -i hosts site.yml --tags install-docker
  
- ansible-playbook -i hosts site.yml --tags install-kubelet
  
- ansible-playbook -i hosts site.yml --tags install-iptables

# Config Firewall on server 

- file firewall.bash: add rule iptables open port.

- Create service "firewall" add to run /etc/firewall.bash.

- Command: service firewall start | stop | status

- iptables command check: iptables -L -n -v

- Disable firewalld on centos, ufw on ubuntu.

- Open port default: 22,80,443,3000,8086.


# Config ssh from Ansible host to Client

- ssh-keygen -t rsa
  
- ssh-copy-id -i ~/.ssh/id_rsa.pub quangch@192.168.17.136
 
- ssh-agent bash

- sudo systemctl reload sshd.service
  



  


