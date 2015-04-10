ansible-armory-init
===================

configures the core security for a new ubuntu server
----------------------------------------------------

*   change root password (long random generated)
    *   passwd
*   update hosts file with current host
    *   update with localhost
    *   update with ansible host
*   update and upgrade
    *   apt-get update
    *   apt-get upgrade
*   install fail2ban
    *   apt-get install fail2ban
*   create system groups needed
    *   sudo addgroup nopwdsudo
    *   sudo addgroup sshlogin
*   create devops user
    *   adduser --home /home/devops --shell /bin/bash --ingroup sudo devops
    *   -- or --
    *   useradd devops
    *   addgroup devops
    *   adduser devops sudo
    *   adduser devops devops
    *   adduser devops nopwdsudo
    *   passwd devops (set something complex and long and record somewhere)
    *   mkdir /home/devops
    *   chown devops:devops /home/devops
*   setup ssh for new user
    *   mkdir /home/devops/.ssh
    *   cat auth-keys.txt > /home/devops/.ssh/authorized_keys
    *   chown devops:devops -R /home/devops
    *   chmod 700 /home/devops/.ssh
    *   chmod 600 /home/devops/.ssh/*
*   disable password login and root access (after testing devops user!)
    *   nano /etc/ssh/sshd_config
    *   PasswordAuthentication yes -> PasswordAuthentication no
    *   ChallengeResponseAuthentication yes -> ChallengeResponseAuthentication no
    *   PermitRootLogin no
    *   X11Forwarding no
    *   UseDNS no
    *   AllowGroups sshlogin
    *   Port {{ non_standard_ssh_port }}
*   lock ssh to specific IPs if desired
    *   AllowUsers devops@(ip) devops@(another-ip)
*   restart the ssh daemon
    *   sudo service ssh restart
*   configure firewall
    *   uwf or iptables?
*   enable automatic security updates?
*   install logwatch or other logging daemon

http://serverfault.com/questions/545978/how-to-handle-ssh-port-changes-with-ansible

https://support.ansible.com/hc/en-us/articles/201957837-How-do-I-split-an-action-into-a-multi-line-format-
https://servercheck.in/blog/yaml-best-practices-ansible-playbooks-tasks

sudo visudo

# members of this group can sudo without a password
%nopwdsudo   ALL=(ALL:ALL) NOPASSWD:ALL


http://managing.blue/2014/09/30/ansible_managed/


lockdown
authorized
foundation
shell
