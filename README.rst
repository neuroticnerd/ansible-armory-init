ansible-armory-init
===================

configures the core security for a new ubuntu server
----------------------------------------------------

*   update and upgrade
    *   apt-get update
    *   apt-get upgrade
*   update hosts file with current host
    *   update with localhost
    *   update with ansible host
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
