# ldap-auth-config Role for Ansible

Set up LDAP user authentication using `debconf` in Debian and Ubuntu.

## Requirements

The role uses [apt module](http://docs.ansible.com/apt_module.html) and [debconf module](http://docs.ansible.com/debconf_module.html) which have basic dependencies. You can use [bootstrap-debian](https://github.com/cederberg/ansible-bootstrap-debian) role to setup common Ansible requirements on Debian-based systems.

## Role Variables

Variables reflect the debconf settings for `ldap-auth-config` package, see also `sudo debconf-show ldap-auth-client`.

See [vars/main.yml](https://github.com/jnv/ansible-role-ldap-auth-client/blob/master/vars/main.yml) for a complete list of variables. Note that `type` key must be present in your variables configuration unless you have [hash merging](http://docs.ansible.com/intro_configuration.html#hash-behaviour) enabled.

## Optional dependencies


## Example Playbook

```
- name: Install and configure LDAP auth client package
  become: true
  roles:
    - role: ldap-auth-client
      ldap_auth_config:
        dbrootlogin:
          type: boolean
          value: false
        rootbinddn:
          type: string
          value: "cn=ldapadm,dc=test,dc=local"
        rootbinpw:
          type: password
          value: superpassw0rd
        dblogin:
          type: boolean
          value: false
        ldapns/base-dn:
          type: string
          value: "dc=test,dc=local"
        ldapns/ldap_version:
          type: select
          value: 3
        ldapns/ldap-server:
          type: string
          value: "ldap://test.ldap.local"
        pam_password:
          type: select
          value: exop
```

Credits
-------

https://github.com/jnv/ansible-role-ldap-auth-client

License
-------
GPLv2
