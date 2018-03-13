mysql
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-mysql.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-mysql)

Provides mysql/mariadb for your system.

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------

- mysql_bind_address: an address where MySQL must bind on.

Dependencies
------------

You can use this role to prepare your system:

- robertdebock.bootstrap

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Example Playbook
----------------

```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.mysql

  tasks:
    - name: Create database
      mysql_db:
        name: bobdata
        state: present

    - name:
      mysql_user:
        name: bob
        password: 12345
        priv: '*.*:ALL'
        state: present
```

Install this role using `galaxy install robertdebock.mysql`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
