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
# add LDAP credential and information on path /etc/dovecot/dovecot-ldap.conf.ext
```bash
vim /etc/dovecot/dovecot-ldap.conf.ext
```
```bash
#hosts = ldaps://192.168.20.61:636
hosts = 192.168.20.61:389
dn = cn=admin,dc=mail,dc=example,dc=com
dnpass = StrongPassword
ldap_version = 3
base = ou=People,dc=mail,dc=example,dc=com
auth_bind = yes
pass_filter = (&(objectClass=inetOrgPerson)(mail=%u))
user_filter = (&(objectClass=inetOrgPerson)(mail=%u))
pass_attrs = uid=user,userPassword=password
```

#Configure for authintication way and file creation for ldap add passdb and userdb
```bash
vim /etc/dovecot/conf.d/auth-ldap.conf.ext
```
```bash
34 passdb {
 35   driver = ldap
 36   args = /etc/dovecot/dovecot-ldap.conf.ext
 37 }
 38 
 39 userdb {
 40   driver = static
 41   args = uid=ops gid=ops home=/home/%u
 42 }
 43 

```
