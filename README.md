# Ansible-docker-k8s-iptalbes
Triển khai hệ thống docker-k8s

# Cấu Trúc triển khai 
- Roles: docker-k8s-iptables

- OS: Triển khai trên hai hệ điều hành Ubuntu16.04 vs CentOS 7.

- Site.yml: File run install Roles: docker, k8s, iptables.

- File hosts: List ip kmaster, knode

- Template: firewall.bash.j2, iptables.sh, /etc/kube/admin.conf, hosts, passdockerlogin.

# Run Ansibles:

- ansible-playbook -i hosts site.yml

- ansible-playbook -i hosts site.yml --user quangch --ask-pass

- ansible -i hosts -m ping all

- ansible-playbook -i hosts site.yml --tags install-docker -------------------run all hosts              

- ansible-playbook -i hosts site.yml --tags install-iptables ------------------run all hosts, install vs open port trước khi install kubeneste.            
  
- ansible-playbook -i hosts site.yml --tags install-kubelet -------------------run all kmaster vs knode host.

- ansible-playbook -i hosts site.yml --tags init-config-kmaster ---------------run kmaster, config kube on master host.

- ansible-playbook -i hosts site.yml --tags init-config-knode -----------------run knode, config kube on knode host vs join knode to kmaster in cluser.File admin.conf.j2, copy từ kmaster /etc/kube/admin.conf.  
- ansible-playbook -i hosts copy-file-conf.yml --tags copy-dockerfile ---------copy dockerfile đến cá Docker host để build docker images.

- ansible-playbook -i hosts copy-file-conf.yml --tags copy-passdocker ---------shell register docker login to docker hub.

- ansible-playbook -i hosts copy-file-conf.yml --tags restart-docker ----------restart docker service, install iptables cần restart docker service.

- ansible-playbook -i hosts copy-file-conf.yml --tags copy-firewall.bash ------copy file bash firewall, add port vs rule cần chạy

# Run Ansibles shell check remote host via ssh:

- ansible -i hosts all -m shell -a 'docker run hello-world'

- ansible -i hosts all -m shell -a "sudo docker build -t apache:0.1 /opt/dockers/apache/." --------------build docker images from dockerfile tren ansible.

- ansible -i hosts all -m shell -a "sudo docker images"

- ansible -i hosts all -m shell -a "sudo docker ps"

- ansible -i hosts all -m shell -a "sudo docker run -d -it -p 443:443 --name nginx-server nginx:1.0" ------run docker images from ansible.

- ansible -i hosts all -m shell -a "cat /opt/dockers/passdocker.txt | docker login --username=quanghong10 --password-stdin" ----ansible command docker login auto


# Config Firewall on server 

- file firewall.bash: add rule iptables open port.

- Create service "firewall" add to run /etc/firewall.bash.

- Command: service firewall start | stop | status

- iptables command check: iptables -L -n -v

- Disable firewalld on centos, ufw on ubuntu.

- Open port default: 22,80,443,3000,8086, 6443, 10250, 10251, 10252, 10255.


# Config ssh from Ansible host to Client

- ssh-keygen -t rsa
  
- ssh-copy-id -i ~/.ssh/id_rsa.pub quangch@192.168.17.136
 
- ssh-agent bash

- sudo systemctl reload sshd.service
  



  


