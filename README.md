# Oracle cloud instances configuration

Reminders and dotfiles for the couple of Ubuntu machines in oracle cloud. 
Fail2ban jails, openvpn, nginx, and the email service.

* The first server hosts the email service and an nginx reverse proxy to the second server.
* The second server hosts the openvpn service and and the nginx server for the website

# Nginx servers config
clone this repo and enable the respective config in each instance
by linking the right file to sites-enabled
