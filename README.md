# Oracle cloud instances configuration

Reminders and dotfiles for the couple of Ubuntu machines in oracle cloud. 
Fail2ban jails, openvpn, nginx, and the email service.

* The first server hosts the email service and an nginx reverse proxy to the second server.
* The second server hosts the openvpn service and and the nginx server for the website

## Configuration
- To allow incoming connections configure the ports and the corresponding security list in the web console
- Reconfigure iptables to allow the traffic


### Nginx servers config - Postfix, dovecot, rspamm, and MySql
clone this repo and enable the respective config in each instance
by linking the right file to sites-enabled

### Email service
* guide used: https://www.linode.com/docs/guides/email-with-postfix-dovecot-and-mysql/
  <br/>
  <br/>
    - dovecot was throwing errors when authenticating throught pam, so i copy and pasted /etc/securetty from StackOverflow
    after checking the original checksum
  <br/>
  <br/>
    - the version of MySql used in the guide used the deprecated function ENCRYPT(), replaced with SHA2('password', 512)
    as per: https://www.linode.com/community/questions/19393/encrypt-function-not-working-following-linode-process-for-mailserver-setup,
    but still didn't work
        - I had to modify the table to have only varchar(512) in the password column and manually encrypted the the password with:
        ```
        sudo doveadm pw -s SHA512-CRYPT
        ```
  <br/>
  <br/>
    - most other steps worked correctly, but the configuration said to use a folder to store incoming mail instead of a file like:
```
mail -f /var/mail/vhosts/example.com/email1
```
  <br/>
  <br/>
    - fixed this by creating a folder with the name of the mail i.e. email1 and a folder inside of this directory called tmp:

```
/var/mail/vhosts/<example@email.com>/<example-user>/tmp
```


