# Ansible-grafana-telegraf-influxdb
Triển khai hệ thống monitor tool grafana

# Cấu Trúc triển khai cài đặt hệ thống Monitor Grafana-Influxdb-Telegraf
- Roles: Grafana - Telegraf - Influxdb - iptables

- OS: Triển khai trên hai hệ điều hành Ubuntu16.04 vs CentOS 7.

- Site.yml: File run install Roles.

- Copy-telegraf.yml: Copy bộ config template đến all agent.

- File hosts: List ip server

- Template: telegraf.conf.j2, firewall.bash.j2, iptables.sh, telegraf_ping.conf, telegraf_snmp.conf, telegraf_window.conf.

# Run Ansibles:

- ansible-playbook -i hosts site.yml

- ansible-playbook -i hosts site.yml --user quangch --ask-pass

- ansible -i hosts -m ping all

- ansible-playbook -i hosts site.yml --tags install-telegraf
  
- ansible-playbook -i hosts site.yml --tags install-grafana
  
- ansible-playbook -i hosts site.yml --tags install-influxdb

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
  



  


