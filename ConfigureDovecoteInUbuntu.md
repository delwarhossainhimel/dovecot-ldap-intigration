## Install in ubuntu
```bash
sudo apt install dovecot-imapd dovecot-pop3d -y 
sudo apt install dovecot-lmtpd 
```
## Configure Dovecote
```bash
vim /etc/dovecot/conf.d/10-auth.conf
```
#Configaration for 10-auth.conf enable ldap on line 124
```bash
124 !include auth-ldap.conf.ext
```

