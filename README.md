# Ansible-LetsEncrypt
Ansible Playbook to generate LE certificat

This playbook generate LE Certificate with dns-01 challenge : use bind and modify zone file with the challenge.

It use directly openssl to generate csr (the ansible module will only be available in v2.4).

It can copy the pem file to HAproxy (adapt it if you want to copy pem file to Apache/NGinx/...).
To generate the pem file, you need lets-encrypt-x3-cross-signed.pem file.

## Run Playbook

### User Key file

First, you need to generate your user.key file :

```
openssl genrsa 4096 > user.key
openssl rsa -in user.key -pubout > user.pub
```

### Call Playbook

```
ansible-playbook letsencrypt.yml -e domain=www.mydomain.com -e dns_file=db.mydomain.com 
```

With copy to HAProxy:
```
ansible-playbook letsencrypt.yml -e domain=www.mydomain.com -e dns_file=db.mydomain.com -e rpin=true
```

