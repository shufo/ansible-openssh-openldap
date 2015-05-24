ansible-openssh-openldap
===================

A playbook for SSH key authentication via OpenLDAP. (Tested on Ubuntu 14.04 Trusty, CentOS 6 and 7.)

## Requirements

- Ansible (Tested on 1.9)

## Overview

It will install OpenLDAP and SSH key authentication setting using LDAP. You can customize it by edit vars file.

## Usage

- Edit vars/main.yml

```
ldap_sampleuser_publickey: "Replace with your Public key"
```

- Test on Vagrant virtual machine(Requires Ansible).

```bash
$ vagrant up
$ ssh 192.168.100.20 -l test
Last login: Fri May 22 18:08:54 2015 from 192.168.100.1
[test@vagrant ~]$ id
uid=1000(test) gid=1000(members) groups=1000(members)
```

- Install to remote server.

Edit `ansible_hosts`.

```
default ansible_ssh_host=127.0.0.1 ansible_ssh_port=22
```

Run playbook.

```bash
ansible-playbook site.yml -i ansible_hosts
```

## vars

```vars/main.yml
---
# ldap server settings
ldap_tld: com
ldap_dc: example
ldap_suffix: "dc={{ ldap_dc }},dc={{ ldap_tld }}"
ldap_root_dn: "cn=Directory Manager,{{ ldap_suffix }}"
ldap_root_password: password
ldap_dir: /var/lib/ldap

ldap_sampleuser_name: test
ldap_sampleuser_password: password
ldap_sampleuser_publickey: "Replace with your Public key"
ldap_sampleuser_uidnumber: 10000
ldap_sampleuser_gidnumber: 10000

ldap_samplegroup_name: members

ldap_users_ou: people
ldap_group_ou: groups

slapd_conf_path: "{{ openldap_conf_dir }}/slapd.conf"

# client side settings
ldap_server_scheme: ldap
ldap_server_host: 127.0.0.1
ldap_server_port: 389
ldap_server_uri: "{{ ldap_server_scheme }}://{{ ldap_server_host }}:{{ ldap_server_port }}"
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
